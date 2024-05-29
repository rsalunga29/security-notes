## Manual Code Review
Look for usage of known insecure functions.

Use `grep` to check the source code recursively. Example:
```bash
grep -r -n 'mysqli_query('
```
The `-r` option tells grep to recursively search all files under the current directory, and the `-n` option indicates that we want grep to tell us the number of the line where the pattern was found.

Once the results are shown, it is important to open the relevant file and read the relevant line to understand the context of the potentially vulnerable line of code.
## Automated Code Review
Uses Static Application Security Testing (SAST) tools.

### SAST Under The Hood
1. Transform the code into an abstract model: Ingest source code, transfer it into a code model called abstract syntax trees (AST)
2. Analyze the AST: Use different analysis techniques to analyze the code model to look for potential vulnerabilities

### Different analysis techniques
1. Semantic Analysis: Can be compared to `grep` in which it finds flaws concerning the use of known insecure code in a local context.
2. Dataflow Analysis: Traces how information flows from user-provided input to potentially vulnerable functions. Basically, sources and sinks concept.
3. Control Flow Analysis: Analyzes the code for race conditions, uninitialized variables, and resource leaks, etc...
4. Structural Analysis: Analyzes specific code structures/blocks of each programming language to look for inconsistencies with safe coding practices.
5. Configuration Analysis: Searches for configuration flaws rather than vulnerabilities in lines of codes.