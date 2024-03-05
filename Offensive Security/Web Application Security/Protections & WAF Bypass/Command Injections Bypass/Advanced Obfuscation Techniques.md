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