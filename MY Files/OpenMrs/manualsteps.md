sudo apt-get update -y
sudo apt-get install openjdk-8-jdk -y
java -version

Install Tomcat 7
----------------

### First, create a user and group for Tomcat with the following command:
sudo groupadd tomcat
sudo useradd -s /bin/false -g tomcat -d /opt/tomcat tomcat

### Next, download the Tomcat 7 with the following command:
wget https://archive.apache.org/dist/tomcat/tomcat-7/v7.0.109/bin/apache-tomcat-7.0.109.tar.gz

### Next, create a directory for Tomcat and extract the downloaded file to /opt/tomcat directory:
sudo mkdir /opt/tomcat
sudo tar -xvzf apache-tomcat-7.0.109.tar.gz -C /opt/tomcat/ --strip-components=1

### Next, navigate to the /opt/tomcat directory and set proper permission and ownership:
-----------------------------------------------------------------------------------------
sudo cd /opt/tomcat
sudo chgrp -R tomcat /opt/tomcat
sudo chmod -R g+r conf
sudo chmod g+x conf
sudo chown -R tomcat webapps/ work/ temp/ logs/



Create a Systemd Service File for Tomcat
----------------------------------------
### Next, you will need to create a systemd service file to manage the Tomcat service. You can create it with the following command:

sudo nano /etc/systemd/system/tomcat.service

Add the following lines:
**************************************
[Unit]
Description=Apache Tomcat Web Application Container
After=network.target
[Service]
Type=forking
Environment=JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-amd64
Environment=CATALINA_PID=/opt/tomcat/temp/tomcat.pid
Environment=CATALINA_HOME=/opt/tomcat
Environment=CATALINA_BASE=/opt/tomcat
Environment=’CATALINA_OPTS=-Xms512M -Xmx1024M -server -XX:+UseParallelGC’
ExecStart=/opt/tomcat/bin/startup.sh
ExecStop=/opt/tomcat/bin/shutdown.sh
User=tomcat
Group=tomcat
UMask=0007
RestartSec=10
Restart=always
[Install]
WantedBy=multi-user.target
***************************************

### Save and close the file then reload the systemd daemon to apply the changes:
sudo systemctl daemon-reload

### Next, start the Tomcat service with the following command:
sudo systemctl start tomcat
sudo systemctl status tomcat


Install OpenMRS
----------------
### First, create a directory for OpenMRS and set proper ownership with the following command:
sudo mkdir /var/lib/OpenMRS
sudo chown -R tomcat:tomcat /var/lib/OpenMRS

### Next, download the latest version of OpenMRS using the following command:
wget https://sourceforge.net/projects/openmrs/files/releases/OpenMRS_Platform_2.5.0/openmrs.war

### Once the download is completed, copy the downloaded file to the Tomcat webapps directory:
sudo cp openmrs.war /opt/tomcat/webapps/

### Next, change the ownership of the openmrs.war file to tomcat:
sudo chown -R tomcat:tomcat /opt/tomcat/webapps/openmrs.war


### Access OpenMRS Installation Wizard
http://your-server-ip:8080/openmrs





