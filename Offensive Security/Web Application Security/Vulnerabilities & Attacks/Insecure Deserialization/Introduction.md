## Serialization vs Deserialization
Serialization is the process of converting complex data structures into a "flatter" format that can be sent or received as a sequential stream of bytes. This makes it much simplier to:
- Write complex data into inter-process memory, a file, or a database.
- Send complex data over a network between different components of an application or in an API call.
When serializing an object, its state if persisted, meaning the object's attributes and its assigned values are preserved.

Deserialization is the process of restoring the byte stream into a fully functional replica of the original data object. The application's logic can then interact with this deserialized object, just like it would with any other object.
![[deserialization-diagram.jpg]]

Many programming languages natively support serialization, some of these languages serialize objects into binary formats, while others use different string formats, with varying degrees of human readability.

There are other terms for serialization, depends on what language is being used, these are "marshalling" (Ruby) and "pickling" (Python).

All of the original object's attributes, including private fields are stored in the serialized data stream. To prevent this from happening, a field must be explicitly marked as "transient" in class declaration.
## What is insecure deserialization?
The insecure deserialization vulnerability occurs when user-controllable data is deserialized by the application without proper validation. This enables an attacker to manipulate serialized objects to pass harmful data into the application.

Additionally, if the application fails to validate the data type, class, or structure of the data, an attacker manipulate the serialized data to make the application instantiate any classes of their own choosing, so long as that class is available to the application. This could potentially lead to remote code execution, privilege escalation, unauthorized access, and many more.

Even if an unexpected class triggers an exception, the damage may have already been done. Many deserialization-based attacks are completed before the process is finished, since the process itself can initiate an attack even if the application's functionality does not directly interact with the malicious object/class. This makes deserialization-based attacks a significant threat even in strongly typed languages.