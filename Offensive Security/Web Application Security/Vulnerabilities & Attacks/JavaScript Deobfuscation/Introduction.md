Before we start learning about deobfuscation, we must first learn about [code ](obsidian://open?vault=security-notes&file=Offensive%20Security%2FWeb%20Application%20Security%2FEvasions%20and%20Bypasses%2FEvasion%20Techniques%2FJavaScript%20Obfuscation%20Techniques%2FIntroduction)obfuscation.

Obfuscation is a technique used to make a script more difficult to read by humans but still work from a technical point-of-view, though performance may be slower. This is usually achieved by using an obfuscation tool.

Code obfuscators often turn the code into a dictionary of all of the words and symbols used within the code and then attempt to rebuild the original code during execution by referring to each word and symbols from the dictionary.

Example:
```javascript
eval(function(p,a,c,k,e,d){e=function(c){return c};if(!''.replace(/^/,String)){while(c--){d[c]=k[c]||c}k=[function(e){return d[e]}];e=function(){return'\\w+'};c=1};while(c--){if(k[c]){p=p.replace(new RegExp('\\b'+e(c)+'\\b','g'),k[c])}}return p}('0.1("2, 3!")',4,4,'console|log|Hello|World'.split('|'),0,{}))
```