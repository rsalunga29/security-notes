OS Command Injection also known as Shell Injection, is a vulnerability that allows an attacker to execute operating system (OS) commands on the server that the application is running on, which typically leads to a full compromise of the application and its data. Often, an attacker can leverage this vulnerability to compromise other parts of the infrastructure and even pivot the attack to other systems within the organization.
## Injecting OS Commands
In this example, an application allows a user to view whether an items is in stock in a particular branch. To do this, the application sends a HTTP request via the URL:
```txt
https://target-website.com/stockStatus?productId=1&storeId=2
```
To provide the information, the application query's a legacy system that is calling out a shell command with product and store ID as arguments and returns the data to the user:
```bash
stockreport.pl 1 2
```
This application implements no defenses against OS command injection, so an attacker can submit malicious input to execute arbitrary commands:
```txt
& echo "hello world" &
```
If the input is submitted in `productId` parameter, the command executed by the application is:
```bash
stockreport.pl & echo "hello world" & 2
```
This will return the following output to the user:
```txt
Error - productID was not provided
hello world
2: command not found
```
