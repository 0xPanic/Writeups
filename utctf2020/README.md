# spooky store
```
It's a simple webpage with 3 buttons, you got this :)
```
Visiting this page revealed a website with 3 clickable buttons that displayed a location's latitute and longitute
![Page](/utctf2020/img/xxe1.png)

Intercepting the request in burpsuite revealed that the POST request is using XML
![POST Request](/utctf2020/img/xxe2.png)

Let's try modifying the post request to be a simple XXE payload to print /etc/passwd (this is the typical payload example that you will find with a google search)


![XXE](/utctf2020/img/xxe3.png)

This worked and printed /etc/passwd, which included the flag

![FLAG](/utctf2020/img/xxe4.png)


# epic admin pwn
```
this challenge is epic i promise
```
For this challenge we are presented with a simple login screen

![Login](/utctf2020/img/sqli1.png)

Start off by trying sql injection to login with user Admin and password 'or '1' ='1 is successful

![Login](/utctf2020/img/sqli2.png)

This gives us a static page, which is basically a dead end. Let's try using sqlmap to try and get something more out of the database.

To do this we intercept the login request in burpsuite and save it to a file called post.txt

![Login](/utctf2020/img/sqli3.png)

From here we run sqlmap. Normally I would use --sql-shell, but that wasn't working so I tried --dump instead.

![Login](/utctf2020/img/sqli4.png)

This successfully dumps the database, which included the flag.
