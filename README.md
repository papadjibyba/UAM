### Install tomcat on ubuntu:

[How To Install Apache Tomcat 8 on Ubuntu 16.04](https://www.digitalocean.com/community/tutorials/how-to-install-apache-tomcat-8-on-ubuntu-16-04)

### GeoSever installation using WAR file 
Download Geoserver from this page: http://geoserver.org/download/

Click on Web archive the Packages section.

Copy the file geoserver.war to the directory that contains your container application’s webapps located in Tomcat folder.

```
/var/lib/tomcat8
```
Start Tomcat.
```
sudo systemctl start tomcat
```
Your container application should unpack the web archive and automatically set up and run GeoServer.

### GeoServer setup for enabling Jsonp

Go to:
```
cd /opt/tomcat/webapps/geoserver/WEB-INF
```
Open with VIM the following file:
```
sudo vim web.xml
```
Uncomment the following lines:
```
<context-param>
    <param-name>ENABLE_JSONP</param-name>
    <param-value>true</param-value>
</context-param>
```
Save by pressing 'ESC' and write:
```
:wq!
```
Restart Tomcat.
```
sudo systemctl restart tomcat
```
### Data 
Italian provinces

GHSL

### Connect Postgis with GeoServer

Make sure you have a Postgis extension on your DB, if you don't, please run the following commands using pgAdmin:
```
CREATE EXTENSION postgis;
CREATE EXTENSION postgis_topology;
```

- Use the workspace called 'yourname'

- Create a new Store (PostGIS Database type) called 'wdpa_db' with the folloing parameters:

```
dbtype: postgis
host: xxx.xxx.xxx
port: 5432
database: yourname
schema: public
user: yourname
password: yourname
```
and publish the protected_areas layer.

### Create GeoServer styles

Set up two styles:

1) Provinces population 2015 (Gradient based on the population 2015)

2) Provinces population 2015 Selection (Yellow Line)

### Pubblish GeoServer layer

- Layer Name: province
- Layer Title: province
- Native SRS: EPSG:32632 UTM zone 32N
- Declared SRS: EPSG:32632 UTM zone 32N

- Apply the style Provinces population 2015 Selection

- Save.




