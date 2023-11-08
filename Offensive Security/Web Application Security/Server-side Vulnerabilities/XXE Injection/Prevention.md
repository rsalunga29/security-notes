Virtually all XXE vulnerabilities are caused by the XML parsing library being used which supports potentially dangerous XML features that the application does not need or intend to use.

The easiest and most effective way to prevent XXE attacks is to disable 

Generally, it is sufficient to disable resolution of external entities and disable support for `XInclude`. This can usually be done via configuration options or by programmatically overriding default behavior.