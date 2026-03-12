# Tomcat Deployment on App Server 1

## Objective
Deploy a Java web application using Tomcat and make it accessible via port 8082.

## Steps

Install Tomcat:

```
sudo yum install tomcat -y
```

Modify Tomcat port in configuration file:

```
/etc/tomcat/server.xml
```

Change connector port:

```
8080 → 8082
```

Start Tomcat service:

```
sudo systemctl start tomcat
sudo systemctl enable tomcat
```

Copy application WAR file from jump host:

```
scp /tmp/ROOT.war tony@stapp01:/tmp
```

Deploy application:

```
sudo cp /tmp/ROOT.war /usr/share/tomcat/webapps/
```

Restart Tomcat:

```
sudo systemctl restart tomcat
```

Verify deployment:

```
curl http://stapp01:8082
```
