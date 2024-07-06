# SQL Injection Writeups

## More SQL; PicoCTF Easy Challenge

There was a sql injection in the login page page. At first could not detect it, as I was getting 500 respone for all the input payloads. At the end I came to know that the database was not mysql because `#` was not working as comment. When I changed `#` to `--`, I was able to grab the flag.
![image](https://github.com/ShudarsanRegmi/ctf-writeups/assets/65646203/e3a87c23-310e-472d-b75c-7cd8fa16df3d)

### payloads
```sql
usernmae=user&passowrd='+or+1=1--
```
