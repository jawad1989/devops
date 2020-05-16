1.  Install Java
```
sudo apt install openjdk-8-jdk
```

2. Postgres Installation
```
sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt/ `lsb_release -cs`-pgdg main" >> /etc/apt/sources.list.d/pgdg.list'

sudo wget -q https://www.postgresql.org/media/keys/ACCC4CF8.asc -O - | sudo apt-key add -

sudo apt-get -y install postgresql postgresql-contrib

sudo systemctl start postgresql

sudo systemctl enable postgresql

```

3. Postgress Configuration
```
sudo passwd postgres
su - postgres
createuser sonar
psql
ALTER USER sonar WITH ENCRYPTED password 'password';
CREATE DATABASE sonar OWNER sonar;
\q
```

4. Install SonarQube Web App
```
sudo apt-get -y install unzip
sudo unzip sonarqube-6.4.zip -d /opt
sudo mv /opt/sonarqube-6.4 /opt/sonarqube -v
```

5. Modify Sonar Properties
```
sudo vi /opt/sonarqube/conf/sonar.properties
```
uncomment the below lines by removing # and add values highlighted yellow
```
sonar.jdbc.username=sonar
sonar.jdbc.password=password
```
Next, uncomment the below line, removing #
```
sonar.jdbc.url=jdbc:postgresql://localhost/sonar
```

6. Creating Sonar as Service

```
sudo vi /etc/systemd/system/sonar.service
```

copy below code once file opens
```
Unit]
Description=SonarQube service
After=syslog.target network.target

[Service]
Type=forking

ExecStart=/opt/sonarqube/bin/linux-x86-64/sonar.sh start
ExecStop=/opt/sonarqube/bin/linux-x86-64/sonar.sh stop

User=root
Group=root
Restart=always

[Install]
WantedBy=multi-user.target

```

Run below commands to start sonar
```
sudo systemctl enable sonar
sudo systemctl start sonar
sudo systemctl status sonar
```

Check logss
```
tail -f /opt/sonarqube/logs/sonar.log

```

Open browser and verify
http://SONARR IP:9000/

