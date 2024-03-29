Once you have detected the template injection potential, the next step is to identify the template engine. Although there are a huge number of templating languages, many of them use very similar syntax that is specifically chosen not to clash with HTML characters.

Identifying the template engine involves analyzing error messages or manually testing various language-specific payloads. Common payloads causing errors include `${7/0}`, `{{7/0}}`, and `<%= 7/0 %>`. Observing the server's response to mathematical operations helps pinpoint the specific template engine.

The diagram below helps us identify if we are dealing with an SSTI vulnerability and also to identify the templating engine.
![[ssti-diagram.png]]

In addition to the above diagram, we can try the following approaches to recognize the technology we are dealing with:
- Check verbose errors for technology names. Sometimes just copying the error in Google search can provide us with a straight answer regarding the underlying technology used
- Check for extensions. For example, `.jsp` extensions are associated with Java. When dealing with Java, we may be facing an expression language/OGNL injection vulnerability instead of traditional SSTI
- Send expressions with unclosed curly brackets to see if verbose errors are generated. Do not try this approach on production systems, as you may crash the webserver.