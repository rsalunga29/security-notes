JavaScript is a loosely typed language, meaning you don't have to specify what type of information will be stored in a variable in advance. This behaviors helps in obfuscating JavaScript codes.

For example, you can cast a variable to String as follows:
```js
//returns "1234"
"" + 1234
1234 + ""

//returns "1234"
[] + 1234
1234 + []

x = "hello"
[1,"a",x] //returns [1, "a", "hello"]
[1,"a",x]+"" //returns "1,a,hello"
```