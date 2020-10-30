# deploy-tomcat

Step-1: Create UBUNTU/CENTOS machine
-------

step-2: Install Java
-------
apt update
sudo apt install openjdk-8-jdk openjdk-8-jre


Step-3: set JAVA_HOME, JRE_HOME, PATH variable
------
ubuntu@ip-10-0-2-252:/usr/lib/jvm$ export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java
ubuntu@ip-10-0-2-252:/usr/lib/jvm$ export JRE_HOME=/usr/lib/jvm/java-8-openjdk-amd64/jre
ubuntu@ip-10-0-2-252:/usr/lib/jvm$ PATH=$PATH:$HOME/bin:$JAVA_HOME

Step-4: Download Tomcat
-------
ubuntu@ip-10-0-2-252:/usr/lib/jvm$ cd /tmp
ubuntu@ip-10-0-2-252:/tmp$  wget https://archive.apache.org/dist/tomcat/tomcat-8/v8.5.35/bin/apache-tomcat-8.5.35.tar.gz


Step-5: Extract tomcat in /opt/tomcat directory
-------
sudo su - root
mkdir -p /opt/tomcat
cd /opt/tomcat
cp /tmp/apache-tomcat-8.5.35.tar.gz .
tar -xzvf apache-tomcat-8.5.35.tar.gz
cd /opt/tomcat/apache-tomcat-8.5.35/


step-6: set the JAVA_HOME & JRE_HOME path in startup and shutdown script for right path.
--------


root@ip-10-0-2-252:/opt/tomcat/apache-tomcat-8.5.35/bin# vi startup.sh
root@ip-10-0-2-252:/opt/tomcat/apache-tomcat-8.5.35/bin# vi shutdown.sh
root@ip-10-0-2-252:/opt/tomcat/apache-tomcat-8.5.35/bin# vi catalina.sh
root@ip-10-0-2-252:/opt/tomcat/apache-tomcat-8.5.35/bin#


JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java
JRE_HOME=/usr/lib/jvm/java-8-openjdk-amd64/jre


step-7: create management user for login into the tomcat management console
------
vi /opt/tomcat/apache-tomcat-8.5.35/conf/tomcat-users.xml

add below line on the below of the script:
<role rolename="manager-script"/>
  <role rolename="manager-jmx"/>
  <role rolename="manager-gui"/>
  <user username="ncodeit" password="ncodeit123" roles="manager-gui, manager-script, manager-jmx, manager-status"/>


Step-7: configure to access from outside
--------
vi /opt/tomcat/apache-tomcat-8.5.35/webapps/manager/META-INF/context.xml
comment these two line:
 <!-- <Valve className="org.apache.catalina.valves.RemoteAddrValve"
         allow="127\.\d+\.\d+\.\d+|::1|0:0:0:0:0:0:0:1" /> -->


Step-8: Start tomcat process
-----------------------------------
/opt/tomcat/apache-tomcat-8.5.35/bin/startup.sh

root@ip-10-0-2-252:/opt/tomcat/apache-tomcat-8.5.35/bin# ./startup.sh
Using CATALINA_BASE:   /opt/tomcat/apache-tomcat-8.5.35
Using CATALINA_HOME:   /opt/tomcat/apache-tomcat-8.5.35
Using CATALINA_TMPDIR: /opt/tomcat/apache-tomcat-8.5.35/temp
Using JRE_HOME:        /usr/lib/jvm/java-8-openjdk-amd64/jre
Using CLASSPATH:       /opt/tomcat/apache-tomcat-8.5.35/bin/bootstrap.jar:/opt/tomcat/apache-tomcat-8.5.35/bin/tomcat-juli.jar
Tomcat started.
root@ip-10-0-2-252:/opt/tomcat/apache-tomcat-8.5.35/bin#

Step-9: verify tomcat process running
-----------------------------------
root@ip-10-0-2-252:/opt/tomcat/apache-tomcat-8.5.35/bin# ps -eaf|grep tomcat

root      7132     1  3 12:47 pts/0    00:00:02 /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java -Djava.util.logging.config.file=/opt/tomcat/apache-tomcat-8.5.35/conf/logging.properties -Djava.util.logging.manager=org.apache.juli.ClassLoaderLogManager -Djdk.tls.ephemeralDHKeySize=2048 -Djava.protocol.handler.pkgs=org.apache.catalina.webresources -Dorg.apache.catalina.security.SecurityListener.UMASK=0027 -Dignore.endorsed.dirs= -classpath /opt/tomcat/apache-tomcat-8.5.35/bin/bootstrap.jar:/opt/tomcat/apache-tomcat-8.5.35/bin/tomcat-juli.jar -Dcatalina.base=/opt/tomcat/apache-tomcat-8.5.35 -Dcatalina.home=/opt/tomcat/apache-tomcat-8.5.35 -Djava.io.tmpdir=/opt/tomcat/apache-tomcat-8.5.35/temp org.apache.catalina.startup.Bootstrap start
root      7178  7085  0 12:48 pts/0    00:00:00 grep --color=auto tomcat
root@ip-10-0-2-252:/opt/tomcat/apache-tomcat-8.5.35/bin#
root@ip-10-0-2-252:/opt/tomcat/apache-tomcat-8.5.35/bin#



Step-10: verify 8080 Port is running
---------------------

root@ip-10-0-2-252:/opt/tomcat/apache-tomcat-8.5.35/bin# netstat -na|grep 8080
tcp6       0      0 :::8080                 :::*                    LISTEN
root@ip-10-0-2-252:/opt/tomcat/apache-tomcat-8.5.35/bin#


Step-11: Access tomcat through browser
--------
http://3.7.73.165:8080/






