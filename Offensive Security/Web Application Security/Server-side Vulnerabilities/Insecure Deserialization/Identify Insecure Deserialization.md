Identifying insecure deserialization is relatively simple. Simply look at all the data being passed into the application and try to identify the anything that looks like serialized data.

> Most cases of insecure deserialization in PHP is found in Base64-encoded value of Cookie HTTP header when serialization-based session mechanism is being used. For other languages, there are other ways to identify a serialized object.

It is also important to know which language the application is using.
## PHP Serialization
PHP uses a mostly human-readable string format, with letters representing the data type and numbers representing the length of each entry.

For example, the `User` object with attributes:
```php
$user->name = "carlos";
$user->isLoggedIn = true;
```
When serialized, this object may look something like this:
```txt
O:4:"User":2:{s:4:"name":s:6:"carlos"; s:10:"isLoggedIn":b:1;}
```
This can be interpreted as follows:
- `O:4:"User"` - An object with the 4-character class name `"User"`
- `2` - the object has 2 attributes
- `s:4:"name"` - The key of the first attribute is the 4-character string `"name"`
- `s:6:"carlos"` - The value of the first attribute is the 6-character string `"carlos"`
- `s:10:"isLoggedIn"` - The key of the second attribute is the 10-character string `"isLoggedIn"`
- `b:1` - The value of the second attribute is the boolean value `true`

> The serialized string for an integer would be `i:123`, notice that it only contains the data type and value, and not including the character length.

The native methods PHP use for serialization are `serialize()` and `unserialize()`. During source code review, it's wise to look for `unserialize()` and start investigating.
## Java Serialization
Some languages, including Java, use binary serialization formats. This is more difficult to read, but can still be identified by recognizing a few tell-tale signs of a captured traffic data:
1. Java objects always begin with the same bytes, which are encoded as `AC ED` or `AC ED 00 05` in hexadecimal and `rO0` in Base64.
2. `Content-Type` header of an HTTP response is set to `application/x-java-serialized-object`.

During source code review, any class that implements the `java.io.Serializable` can be serialized and deserialized. The following methods can be the source of this vulnerability as well:
- `XMLdecoded`
- `XStream` with `fromXML` method (XStream version <= v1.46)
- `ObjectInputStream` with `readObject`
- Uses of `readObject`, `readObjectNodData`, `readResolve`, or `readExternal` (used to read and deserialized data from an `InputStream`)
- `ObjectInputStream.readUnshared`
## Python Serialization
During code review, look for the following code snippets:
- Uses of `pickle` with `load()`.
- Uses of `PyYAML` with `load()`.
- Uses of `jsonpickle` with `encode` or `store` methods.
Additionally, if the traffic data contains the symbol dot `.` at the end, it's very likely that the data was sent in serialization.
## .NET Serialization
During code review, look for the following code snippets:
- Uses of `TypeNameHandling`.
- Uses of `JavaScriptTypeResolver`.
- Any serializers where the type of set by a user-controlled variable.
Additionally, look for traffic data that contains a Base64-encoded content that starts with `AAEAAAD/////`. Then look for the `TypeObject` and `$type:` content in the decoded string.