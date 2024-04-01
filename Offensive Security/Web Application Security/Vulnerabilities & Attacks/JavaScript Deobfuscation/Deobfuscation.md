Just as there are tools to obfuscate code automatically, there are tools to beautify and deobfuscate the code automatically.
## Beautify
This one is the simplest and works with minified JavaScript code. Tools like [Prettier](https://prettier.io/playground/) and [Beautifier](https://beautifier.io/) makes it easier. However, if you're using Firefox, we can open the browser debugger with [Ctrl +Shift+Z], and then click on a minified script which will show the script in its original formatting, but by clicking `{ }` button located at the bottom left, it will "Pretty Print" the script into its proper JavaScript formatting, making the code easier to read.
## Unpack
Tools like [UnPacker](https://matthewfl.com/unPacker.html) can easily deobfuscate JavaScript codes that are obfuscated using the "packing" technique. Another way of unpacking such code is to find the return value at the end and use console.log to print it instead of executing it.
## JSFuck
Tools like [Decoder JSFuck](https://enkhee-osiris.github.io/Decoder-JSFuck/) can deobfuscate JavaScript codes that are obfuscated using JSFuck.
## Advanced
Though these tools are great for clearing up obfuscated code. Once a code has been obfuscated and encoded multiple times, it would become much difficult to automate the deobfuscation process. This is specially true if the code was obfuscated using a custom tool.

In order to deobfuscate such codes, we would need to manually reverse engineer the code to understand how it was obfuscated and its functionality.