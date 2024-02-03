## Serialization vs Deserialization
Serialization is the process of converting complex data structures into a "flatter" format that can be sent or received as a sequential stream of bytes. This makes it much simplier to:
- Write complex data into inter-process memory, a file, or a database.
- Send complex data over a network between different components of an application or in an API call.
When serializing an object, its state if persisted, meaning the object's attributes and its assigned values are preserved.

Deserialization is the process of restoring the byte stream into a fully functional replica of the original data object. The application's logic can then interact with this deserialized object, just like it would with any other object.
![[deserialization-diagram.jpg]]

Many programming languages natively support serialization, some of these languages serialize objects into binary formats, while others use different string formats, with varying degrees of human readability.

All of the original object's attributes, including private fields are stored in the serialized data stream. To prevent this from happening, a field must be explicitly marked as "transient" in class declaration.

There are other terms for serialization, depends on what language is being used, th are "marshalling" (Ruby) and "pickling" (Python).