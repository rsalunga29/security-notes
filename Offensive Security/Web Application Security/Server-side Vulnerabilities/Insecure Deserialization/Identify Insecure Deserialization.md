Identifying insecure deserialization is relatively simple. Simply look at all the data being passed into the application and try to identify the anything that looks like serialized data.

It is also important to know which language the application is using.
## PHP Serialization
PHP uses a mostly human-readable string format, with letters representing the data type and numbers representing the length of each entry.