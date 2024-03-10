Other commonly blacklisted characters includes the slash (`/`) or backslash (`\`). There are a couple of ways to bypass such filters for this characters.
## Utilizing Linux Environment Variables
Just like how `$IFS` can be as a replacement for the space character, the `$PATH` environment variable can also be used to replace slashes. If we look at the `$PATH` variable in Linux, it would be echo following:
```bash
/usr/local/bin:/usr/bin:/bin:/usr/games
```
In order to use the slashes in the results, we will use a special technique to isolate individual characters. So if we do `echo ${PATH:0:1}`, it means that the string will start at `0` index character and take a length of `1` which will end up with only the `/` character. We can also use the same with `$HOME` and `$PWD` environment variables as well.

We can also use the same concept to get a semicolon character, by using the `$LS_COLORS` environment variable: `echo ${LS_COLORS:10:1}`.
> Note: When we use the above command in our payload, we will not add echo, as we are only using it in this case to show the outputted character.
## Utilizing Windows Environment Variables
The same concept will work on Windows as well. The Windows variable `%HOMEPATH%` will return the absolute path of the current user's home directory (e.g `\Users\htb-student`). As such, if we use `%HOMEPATH:~6,-11%` it will return the value `\`.

We can achieve the same thing using the same variable in Windows Powershell. With PowerShell, a word is considered an array, so we have to specify the index of the character we need. So for example, we will do `$env:HOMEPATH[0]` instead.
## Character Shifting
Character Shifting is a technique that is used in the following command to shift the character that we pass by `1`.
```bash
echo $(tr '!-}' '"-~'<<<[)
```
In the example above, we specified the `[` character, which is on 91 in the ASCII table, and after it is `\` which is 92 on the ASCII table.