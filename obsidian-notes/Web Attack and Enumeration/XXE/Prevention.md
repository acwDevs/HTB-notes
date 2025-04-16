

[OWASP's XXE Prevention Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/XML_External_Entity_Prevention_Cheat_Sheet.html#php)

## Avoiding Outdated Components

DO NOT USE OUTDATED VERSIONS OF XML

For example, PHP's [libxml_disable_entity_loader](https://www.php.net/manual/en/function.libxml-disable-entity-loader.php) function is deprecated since it allows a developer to enable external entities in an unsafe manner, which leads to XXE vulnerabilities.

In addition to updating the XML libraries, we should also update any components that parse XML input, such as API libraries like SOAP


## Using Safe XML Configurations

- Disable referencing custom `Document Type Definitions (DTDs)`
- Disable referencing `External XML Entities`
- Disable `Parameter Entity` processing
- Disable support for `XInclude`
- Prevent `Entity Reference Loops`

Another thing we saw was Error-based XXE exploitation. So, we should always have proper exception handling in our web applications and `should always disable displaying runtime errors in web servers`.

