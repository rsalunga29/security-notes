The easiest and most effective way to prevent XXE attacks is to configure the XML parsing libraries and XML configurations to:
- Disable DTD support and referencing custom DTDs.
- Disable the external entity functionality and referencing of external XML entities.
- Disable parameter entity processing.
- Disable support for `XInclude`.
- Prevent entity reference loops.

Finally, it is advisable to avoid using outdated components. For example, PHP's [libxml_disable_entity_loader](https://www.php.net/manual/en/function.libxml-disable-entity-loader.php) function is deprecated since it allows a developer to enable external entities in an unsafe manner, which leads to XXE vulnerabilities.