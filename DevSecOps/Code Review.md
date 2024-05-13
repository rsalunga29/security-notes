## Manual
Look for usage of known insecure functions.

Use `grep` to check the source code recursively. Example:
```bash
grep -r -n 'mysqli_query('
```
## Automated
Uses Static Application Security Testing (SAST)

SAST Under The Hood:
1. Transform the code into an abstract model: Ingest source code, transfer it into a code model called abstract syntax trees (AST)
2. Analyze the AST: Use different analysis techniques to analyze the code model to look for potential vulnerabilities

Different analysis techniques:
1. Semantic Analysis: Can be compared to `grep` in which it finds flaws concerning the use of known insecure code in a local context.
2. Dataflow Analysis: Traces how information flows from user-provided input to potentially vulnerable functions. Basically, sources and sinks concept.