According to Apache, [AJP](https://cwiki.apache.org/confluence/display/TOMCAT/Connectors) (or JK) is a wire protocol. It is an optimized version of the HTTP protocol to allow a standalone web server such as Apache to talk to Tomcat. Historically, Apache has been much faster than Tomcat at serving static content. The idea is to let Apache serve the static content when possible but proxy the request to Tomcat for Tomcat-related content.

When we come across an open AJP proxy port (8009 TCP), we can use Nginx with the `ajp_module` to access the "hidden" Apache Tomcat Manager, giving access to administrative panels, applications, and websites that would be otherwise inaccessible.
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
```bash
sudo docker run -it --rm -p 8009:8009 -v `pwd`/tomcat-users.xml:/usr/local/tomcat/conf/tomcat-users.xml --name tomcat "tomcat:8.0"
```
## Nginx Reverse Proxy and AJP
Next, we need to download the Nginx source code and the AJP module
```bash
wget https://nginx.org/download/nginx-1.21.3.tar.gz
git clone https://github.com/dvershinin/nginx_ajp_module.git

tar -xzvf nginx-1.21.3.tar.gz
```
Then we need to compile the source code with the AJP module
```bash
cd nginx-1.23.1
sudo apt install libpcre3-dev
./configure --add-module=`pwd`/../nginx_ajp_module --prefix=/etc/nginx --sbin-path=/usr/sbin/nginx --modules-path=/usr/lib/nginx/modules
make
sudo make install
```
Next we edit the `/etc/nginx/conf/nginx.conf` and comment out the entire `server` block and append the following lines inside the `http` block:
```conf
upstream tomcats {
	server <TARGET_SERVER>:8009;
	keepalive 10;
}
server {
	listen 80;
	location / {
		ajp_keep_conn on;
		ajp_pass tomcats;
	}
}
```
Then we simply start Nginx and confirm everything is working correctly by using cURL
```bash
sudo nginx
curl <TARGET_SERVER>:8009
```
## Apache Reverse Proxy and AJP
The same technique can also be done using Apache. First, we install and enable all required modules.
```bash
sudo apt install libapache2-mod-jk
sudo a2enmod proxy_ajp
sudo a2enmod proxy_http
```
Then we configure the `/etc/apache2/sites-available/ajp-proxy.conf`
```bash
export TARGET="<TARGET_SERVER>"
echo -n """<Proxy *>
Order allow,deny
Allow from all
</Proxy>
ProxyPass / ajp://$TARGET:8009/
ProxyPassReverse / ajp://$TARGET:8009/""" | sudo tee /etc/apache2/sites-available/ajp-proxy.conf
sudo ln -s /etc/apache2/sites-available/ajp-proxy.conf /etc/apache2/sites-enabled/ajp-proxy.conf
```
Then we simple start Apache and confirm everything is working correctly by using cURL
```bash
sudo systemctl start apache2
curl <TARGET_SERVER>:8009
```