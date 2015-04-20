# docker-thingworx
A dockerfile to dockerize Thingworx plateform

Why ?
-----

Thingworx is a plateform dedicated to design and run IoT/M2M applications. See http://www.thingworx.com/

**TW is an under licenced software, you need to buy it.**

I have to use it in my work at Rtone (http://rtone.fr) and a Docker container should be useful to share the plateform with colleagues.

Content of the container
------------------------

TW is a java based webapp. It runs on a tomcat-7/jre-7 environnement with some jvm options (not sure all are really needed but I followed the doc). TW need also 2 directories to store its data.

I picked a tomcat-7 Dockerfile and customized it to deploy TW. It's very simple and perhaps could be improved. Feel free to fork/PR.

I add a tomcat-users.xml with a admin/admin user to check Tomcat manager during my tests.

HowTo
-----

 * You need to add the Thingworx.war file in the build directory.
 * docker build -t thingworx .
 * docker run -d -p 8080:8080 thingworx
 * connect to http://localhost:8080
 * default account is Administrator/admin

You should use Docker shared volumes to get the TW storage directories (/ThingworxStorage and ThingworxBackupStorage) outside of the container. Example : docker run -d -p 8080:8080 -v $HOME/TW/ThingworxStorage:/ThingworxStorage -v $HOME/TW/ThingworxBackupStorage:/ThingworxBackupStorage thingworx
