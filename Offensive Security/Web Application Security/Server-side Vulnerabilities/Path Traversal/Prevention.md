The most effective way to prevent a Path Traversal vulnerability is to avoid passing user-supplied input to filesystem APIs altogether. If you can't avoid this, use two layers of defense to prevent such attacks:
- Validate the user input before processing it. Ideally, compare the user input with a whitelist of permitted values, otherwise, verify that the input contains only permitted content, such as alphanumeric characters only.
- After validating the supplied input, append the input to the base directory and use a platform filesystem API to canonicalize the path. Verify that the canonicalized path starts with the expected base directory.

Below is an example of a simple Java code to validate the canonical path of a file based on the user input:
```java
File file = new File(BASE_DIRECTORY, userInput); if (file.getCanonicalPath().startsWith(BASE_DIRECTORY)) { // process file }`
```
