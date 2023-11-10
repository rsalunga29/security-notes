Business logic vulnerabilities, also known as "application logic vulnerabilities", or "simply logic flaws", are flaws in the design and implementation of an application, that allows an attacker to elicit unintended behavior from legitimate functionalities to achieve a malicious goal. These flaws are generally the result of design and development teams failing to anticipate unusual user behavior and application states that may occur, and consequently, failing to handle them safely.


Logic flaws are often invisible to users who normally use the applications. However, an attacker may exploit behavioral quirks by interacting with the application in ways that developers never intended.

This type of vulnerability can be extremely diverse and often unique to an application and its specific functionality. Identifying them often requires a certain amount of human knowledge, such as business domain expertise. This makes it difficult for automated vulnerability scanners to detect. However, a great target for bug bounty hunters and manual testers in general.
## Note
In this context, the term "business logic" simply refers to the set of rules that define how the application operates or react when a given scenario occurs.

The main purpose of "business logic" to enforce rules and constraints that were defined when designing the application of functionality. For example, applying proper validation to prevent users from making arbitrary changes to transaction-critical values.