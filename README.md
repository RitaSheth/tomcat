# tomcat
#create tomcat user and directory
#sudo useradd -m -d /opt/tomcat -u -s /bin/false tomcat
#updating & installing package 
#sudo apt update && sudo apt install default-jdk -y
#java -version
# cd tmp dirtory cd /tmp
# wget https://dlcdn.apache.org/tomcat/tomcat-10/v10.0.20/bin/apache-tomcat-10.0.20.tar.gz
#unzip tomcat files to /opt/tomcat 
sudo tar xzvf apache-tomcat-10*tar.gz -C /opt/tomcat --strip-components=1 
#changing the owner&group and providinfg execution permission
sudo chown -R tomcat:tomcat /opt/tomcat/
sudo chmod -R u+x /opt/tomcat/bin
# created service file and add service file to it
[Unit]
Description=Tomcat
After=network.target

[Service]
Type=forking

User=tomcat
Group=tomcat

Environment="JAVA_HOME=/usr/lib/jvm/java-1.11.0-openjdk-amd64"
Environment="JAVA_OPTS=-Djava.security.egd=file:///dev/urandom"
Environment="CATALINA_BASE=/opt/tomcat"
Environment="CATALINA_HOME=/opt/tomcat"
Environment="CATALINA_PID=/opt/tomcat/temp/tomcat.pid"
Environment="CATALINA_OPTS=-Xms512M -Xmx1024M -server -XX:+UseParallelGC"

ExecStart=/opt/tomcat/bin/startup.sh
ExecStop=/opt/tomcat/bin/shutdown.sh

RestartSec=10
Restart=always

[Install]
WantedBy=multi-user.target
#demon restart
sudo systemctl daemon-reload
#start and enable tomcat service
sudo systemctl start tomcat
sudo systemctl status tomcat
sudo systemctl enable tomcat

#take the <public ip> http://<publicip>:8080
