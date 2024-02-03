## Cause
This vulnerability typically occurs due to lack of proper validation on the deserialized data. However, there will be times this is ineffective since its impossible to validate or sanitize for every scenario.

These validations are also flawed as they rely on checking the data after it has been deserialized, which in many cases will be too late to prevent the attack. Additionally, the vulnerability may also arise because developers might think that users cannot read or manipulate binary serialization format. While it may require more effort, exploitation is still possible.

Furthermore, modern applications uses a number of dependencies, which may have their own dependencies as well. This creates a massive pool of classes, methods, and objects that is difficult to manage securely. As a result of this, an attacker can chain together a series of unexpected class or method invocations, passing data into a sink that is completely unrelated to the initial source.

In short, it can be argued that it is not possible to securely deserialize untrusted input.
## Prevention
This vulnerability can be avoided by implementing proper validation, however, it is important to remember that any validation must take place before the beginning of the deserialization process.

Deserialization of user input should be avoided. If it cannot be avoided, robust measures must be implemented to make sure that the data has not been tampered with. Such as implementing a digital signature to verify the data's integrity.

Avoid using generic deserialization features/functions as serialized data from these may contain all attributes of the original object, including any private fields that contains sensitive information. Instead, create your own class-specific serialization methods.