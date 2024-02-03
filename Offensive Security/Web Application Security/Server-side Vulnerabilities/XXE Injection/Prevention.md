The easiest and most effective way to prevent XXE attacks is to configure the XML parser to disallow custom DTDs, disable DTD support, and disable the external entity functionality.

Additionally, it is also advisable to disable potentially dangerous features from XML parsing library that the application does not need or intend to use.

Generally, it is sufficient to disable resolution of external entities and disable support for `XInclude`. This can usually be done via configuration options or by programmatically overriding default behavior.