# SQL Injection Writeups

## 1. More SQL; PicoCTF Easy Challenge

There was a sql injection in the login page page. At first could not detect it, as I was getting 500 respone for all the input payloads. At the end I came to know that the database was not mysql because `#` was not working as comment. When I changed `#` to `--`, I was able to grab the flag.
![image](https://github.com/ShudarsanRegmi/ctf-writeups/assets/65646203/e3a87c23-310e-472d-b75c-7cd8fa16df3d)

### Payloads
```sql
usernmae=user&passowrd='+or+1=1--
```
### 2. SQLiite  picoCTF challenge
Had a login page with field username and password. Although it didn't show any changed response upon trying test payloads. It was indeed vulnerable to SQLi. Got the flag by trying the simple payload. The main catch here could be the use of database sqlite. Sqlite doesn't use `#` as comment. So, you have to use `--` instead.
## Payloads
```http
username=admin'+or+1=1--&password=asdf&debug=0
```
![image](https://github.com/ShudarsanRegmi/ctf-writeups/assets/65646203/7e18200b-3491-4423-bde7-3ef0cce0ed1a)

