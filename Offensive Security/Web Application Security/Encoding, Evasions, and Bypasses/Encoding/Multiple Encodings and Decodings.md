Its common to abuse multiple encodings to bypass security measures. Some examples are as follows:

**Base64 and URL Encoding**
In this example, a parameter value is Base64-encoded:
```txt
http://mywebsite/login.php?param=Rk9SVy1VUkw/Y2F0PWNsb3ducw==
```
If its sent over URL, the results will be:
```txt
http://mywebsite/login.php?param=Rk9SVy1VUkw%2FY2F0PWNsb3ducw%3D%3D
```

**Parameter Encoding**
Additionally, a simple parameter can be a structured parameter. For example, the following cookie value:
```http
...SESSION=dXNlcm5hbWU6Y2xvd247cGFzc3dvcmQ6dGhlQ2xvd24h
```
It may appear like a random value, but it can be decoded to:
```http
...SESSION=username:clown;password:theClown!
```