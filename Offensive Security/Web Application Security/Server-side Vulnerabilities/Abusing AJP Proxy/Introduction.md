According to Apache, [AJP](https://cwiki.apache.org/confluence/display/TOMCAT/Connectors) (or JK) is a wire protocol. It is an optimized version of the HTTP protocol to allow a standalone web server such as Apache to talk to Tomcat. Historically, Apache has been much faster than Tomcat at serving static content. The idea is to let Apache serve the static content when possible but proxy the request to Tomcat for Tomcat-related content.

An open AJP ports (8009 TCP) can be used to access the "hidden" Apache Tomcat Manager behind it. Configurating our own Nginx or Apache webserver with AJP modules would give us access to administrative panels, applications, and websites that would be otherwise inaccessible.
## Initial Setup
First we have to create a file called `tomcat-users.xml` with the following content:
```xml
<tomcat-users>
	<role rolename="manager-gui"/>
	<role rolename="manager-script"/>
	<user username="tomcat" password="secret" roles="manager-gui,manager-script"/>
</tomcat-users>
```
Then make sure we have Docker installed, once confirmed, spin up a Docker instance.
```nix
sudo docker run -it --rm -p 8009:8009 -v `pwd`/tomcat-users.xml:/usr/local/tomcat/conf/tomcat-users.xml --name tomcat "tomcat:8.0"
```