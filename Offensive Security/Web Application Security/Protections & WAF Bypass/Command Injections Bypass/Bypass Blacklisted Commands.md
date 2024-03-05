## Linux & Windows
One very common obfuscation techniques is inserting certain characters within our command that are usually ignored by Bash or Powershell and will execute the same command as if they were not there. Some of these characters are single-quote and a double-quote, in addition to a few others. Example below:
```http
POST / HTTP/1.1
Host: target-website.com
...

ip=127.0.0.1%09w'h'o'am'i
```
> Tip: The important things to remember are that we cannot mix types of quotes and the number of quotes must be even.
## Linux Only
We can also insert a few Linux-only characters in the middle of commands, and the bash shell would ignore it and execute the command. These characters include the backslash and the positional parameter character (`$@`).