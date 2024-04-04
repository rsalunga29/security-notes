Regular Expressions or RegEx is a special sequence of characters used for describing a search pattern. It commonly used when defining rules of different filtering mechanisms. Mastering RegEx is fundamental to understand how to bypass filters.

## Regex Engine
The implementation of regex functionality is often called regex engine, which basically tries to match the pattern (regex) to a given string.

There are two main types of regex engines : DFA (text-directed) and NFA (regex-directed). The DFA engine is faster than NFA because of its deterministic approach, but does not support useful features like **lazy quantifiers** and **backreferences**. While the NFA works the way humands tend to do: "regex-directed".

The following is a list of programs that uses the engines:
**DFA**
- awk
- egrep
- MySQL
- Procmail

**NFA**
- .NET Languages
- Java
- Perl
- PHP
- Python
- PCRE library,
- grep
- vi
- etc...
## Regex Symbols
Regex is known as a "symbolic language", below is a table of regex symbols and their meanings.

| Character | Name                            | Meaning                                                                                |
| --------- | ------------------------------- | -------------------------------------------------------------------------------------- |
| `^`       | Caret                           | The position at the START of the line.                                                 |
| `$`       | Dollar                          | The position at the END of the line.                                                   |
| `()`      | Opening/closing parenthesis     | Start/close a characters group.                                                        |
| `[]`      | Opening/closing square brackets | Start/close a characters class.                                                        |
| `{}`      | Opening/closing curly brace     | Start/close repetitions of a characters class.                                         |
| `?`       | Question mark                   | One or zero (optional) of the immediately-preceding item (char or group).              |
| `+`       | Plus                            | One or more of the immediately-preceding item (char or group).                         |
| `*`       | Star or asterisk                | Any number, including none, of the immediately-preceding item (char or group).         |
| `.`       | Dot or period                   | Shorthand for a character class that matches any character.                            |
| `\`       | Backslash                       | Escape special characters.                                                             |
| `\|`      | Vertical bar or pipe            | It means OR. Combines multiple expressions in one that matches any of the single ones. |
## Shorthand Character Class
Since there are some character classes frequently used, there are also related shorthand classes that are useful to decrease the size and increase the readability of a regex.

| Character | Name                   | Meaning                                                                                     |
| --------- | ---------------------- | ------------------------------------------------------------------------------------------- |
| `^`       | Caret                  | If at the beginning of the character class, it means to reverse the matching for the class. |
| `\d`      | Digit                  |                                                                                             |
| `\D`      | Non-digit              |                                                                                             |
| `\w`      | Part-of-word character |                                                                                             |
| `\W`      | Non-word character     |                                                                                             |
| `\s`      | Whitespace             |                                                                                             |
| `\S`      |                        |                                                                                             |