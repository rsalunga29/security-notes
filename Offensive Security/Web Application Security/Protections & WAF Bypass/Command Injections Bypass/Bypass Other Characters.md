Other commonly blacklisted characters includes the slash (`/`) or backslash (`\`). There are a couple of ways to bypass such filters for this characters.
## Utilizing Linux Environment Variables
Just like how `$IFS` can be as a replacement for the space character, the `$PATH` environment variable can also be used to replace slashes. If we look at the `$PATH` variable in Linux, it would be echo following:
```nix
/usr/local/bin:/usr/bin:/bin:/usr/games
```
In order to use the slashes in the results, we will use a special technique to isolate individual characters. So if we do `echo ${PATH:0:1}`, it means that the string will start at `0` index character and take a length of `1` which will end up with only the `/` character. We can also use the same with `$HOME` and `$PWD` environment variables as well.

We can also use the same concept to get a semicolon character, by using the `$LS_COLORS` environment variable: `echo ${LS_COLORS:10:1}`.
> 