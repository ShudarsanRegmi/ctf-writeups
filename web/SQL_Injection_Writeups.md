![image](https://github.com/ShudarsanRegmi/ctf-writeups/assets/65646203/adb6d292-2342-4cc7-901b-434eab54a73d)# SQL Injection Writeups

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
**Flag:**picoCTF{L00k5_l1k3_y0u_solv3d_it_ec8a64c7}
![image](https://github.com/ShudarsanRegmi/ctf-writeups/assets/65646203/7e18200b-3491-4423-bde7-3ef0cce0ed1a)

## 3. Irish Name Repo 1, Very simple SQli based challenge

Just a simple payload in login form yielded

### Payloads

```http
username=admin'+or+1=1--&password=admin&debug=1
```
![image](https://github.com/ShudarsanRegmi/ctf-writeups/assets/65646203/7ccc383c-b2c7-4f19-9852-1be5c332ee17)

### 4. Web Gautlet 2
It was a easy level sql injection challenge in picoCTF. The main challenge here was that the common payloads that are used for sql injections were being filtered out. Keywrods like admin,and special symbols like = < > ; or were getting filtered. So the challenge was to bypass this very simple filter implementation.
Manged to get the flag with the payload below. 
```
user=ad'||'min&pass=a'+is+not+'b
```
![image](https://github.com/ShudarsanRegmi/ctf-writeups/assets/65646203/05a0c89f-65c5-44f2-96ae-63ec7dad2f4d)

Finally got the flag in /filter.php
```
picoCTF{0n3_m0r3_t1m3_86f3e77f3c5a076866a0fdb3b29c52fd}
```
