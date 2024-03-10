Extensible Stylesheet Language Transformations (`XSLT`) is an XML-based language usually used when transforming XML documents into HTML, another XML document, or PDF. XSLT Injection can occur when arbitrary XSLT file upload is possible or when an application generates the XSLT Transformation's XML document dynamically using non-validated input from the user.
## Installation of required packages
```bash
sudo apt install default-jdk libsaxon-java libsaxonb-java
```
## C
```xml
<?xml version="1.0" encoding="UTF-8"?>
<catalog>
  <cd>
    <title>Empire Burlesque</title>
    <artist>Bob Dylan</artist>
    <country>USA</country>
    <company>Columbia</company>
    <price>10.90</price>
    <year>1985</year>
  </cd>
  <cd>
    <title>Hide your heart</title>
    <artist>Bonnie Tyler</artist>
    <country>UK</country>
    <company>CBS Records</company>
    <price>9.90</price>
    <year>1988</year>
  </cd>
  <cd>
    <title>Greatest Hits</title>
    <artist>Dolly Parton</artist>
    <country>USA</country>
    <company>RCA</company>
    <price>9.90</price>
    <year>1982</year>
  </cd>
</catalog>
```