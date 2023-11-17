Cross-origin Resource Sharing (CORS) is a browser mechanism which enables controlled access to resources located outside of a given domain. While it extends and adds flexibility to the [Same-Origin Policy](obsidian://open?vault=security-notes&file=Offensive%20Security%2FWeb%20Application%20Security%2FClient-side%20Vulnerabilities%2FCross-Origin%20Resource%20Sharing%20(CORS)%2FSame-origin%20Policy), it also provides a potential for cross-domain attacks if poorly configured and implemented.

The CORS protocol uses a suite of HTTP headers that define trusted origins and associated properties. These are combined in a header exchange between a browser and the cross-origin website that it is trying to access.

<!-- @TODO: Link CSRF from Client-side vulnerabilities -->
CORS also does not provide protection against Cross-Site Request Forgery (CSRF) attacks, this is a common misconception. As poorly configured CORS may increase the possibility of CSRF attacks or worsen their impact.

There are also various ways to perform CSRF attacks without using CORS, including simple HTML forms and cross-domain resource includes.