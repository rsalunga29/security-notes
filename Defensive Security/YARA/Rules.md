The proprietary language that Yara uses for rules is fairly trivial to pick up, but hard to master. This is because, rules are only as effective as a researcher's understanding of the patterns they want to search for.

The `.yar` is the standard file extensions for all Yara rules.

Using a Yara rule is simple. Every `yara` command requires two arguments to be valid, these are:  
1. The rule file we create.
2. Name of file, directory, or process Id to use the rule for.

For example, if we wanted to use `custom-rule.yar` on directory "custom_directory", the command will be the following:
```bash
yara custom-rule.yar custom_directory
```
## Yara Rule Anatomy
![[yara-rule-anatomy.png]]
## Example Rule
Every rule must have a name and condition. For example, the following is an example of a custom Yara rule:
```yara
rule examplerule {
	condition: true
}
```
The name of the rule is `examplerule` and we have a condition named `condition`, which is set to `true`.

Simply, the rule we have made checks to see if the file/directory/PID that we specify exists via `condition: true`. If the file does exist, we are given the output of `examplerule`.
## Rule Conditions
Yara has a few conditions which can be read [here](https://yara.readthedocs.io/en/stable/writingrules.html). Below are some of most common conditions:
### Meta
This section of a Yara rule is reserved for descriptive information by the author of the rule. For example, the `desc` which is short for description, can be used to summarize what the rule is for.
### Strings
We can use strings to search for a specific text or hexadecimal in files or programs. For example:
```yara
rule helloworld_checker {
	strings:
		$hello_world = "Hello, World!"

	condition:
		$hello_world
}
```
We also added a condition to make the rule valid. Essentially, if any file has the string "Hello World!" then the rule will match. However, this will not match the same string in lowercase or uppercase.

To solve this, wee add the condition `any of them` to allow multiple strings to be searched for. For example:
```yara
rule helloworld_checker {
	strings:
		$hello_world = "Hello, World!"
		$hello_world_lcase = "hello, world!"
		$hello_world_ucase = "HELLO, WORLD!"

	condition:
		any of them
}
```
## Conditions
Much like regular programming, Yara also uses the following operators:
- `<=` - less than or equal to
- `=>` - greater than or equal to
- `!=` - not equal to

For example:
```yara
rule helloworld_checker {
	strings:
		$hello_world = "Hello, World!"

	condition:
		#hello_world <= 10
}
```
The above rule will search for the "Hello, World!" string and will only match if there are less than or equal to ten occurrences of the string.
## Combining Keywords
We can also use the following keywords to combine conditions:
- and
- not
- or

For example, if we want to check if the file has a string and is of a certain file size.
```yara
rule helloworld_checker {
	strings:
		$hello_world = "Hello, World!"

	condition:
		$hello_world and filesize < 10KB
}
```
The above rule will only match if both of the conditions are true.