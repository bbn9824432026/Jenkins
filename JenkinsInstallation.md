---

## ✅ 3.1 Introduction
> Jenkins is easy to install and can be up and running in minutes. This chapter covers installation on local and production environments including system maintenance tasks.

---

## 📥 3.2 Downloading and Installing Jenkins

### Check Java version:
```bash
java -version
```

### Run Jenkins from WAR file:
```bash
java -jar jenkins.war
```

---

## 🛠️ 3.3 Preparing a Build Server for Jenkins

### Create a dedicated Jenkins user:
```bash
sudo groupadd build
sudo useradd --create-home --shell /bin/bash --groups build jenkins
```

### Set environment variables:
In `.bashrc`:
```bash
export JAVA_HOME=/usr/local/java/jdk1.6.0
export PATH=$JAVA_HOME/bin:$PATH
```

---

## 🗂️ 3.4 The Jenkins Home Directory

### Override default home:
```bash
export JENKINS_BASE=/usr/local/jenkins
export JENKINS_HOME=/var/jenkins-data
java -jar ${JENKINS_BASE}/jenkins.war
```

### For Tomcat:
Create `jenkins.xml`:
```xml
<Context docBase="../jenkins.war">
  <Environment name="JENKINS_HOME" type="java.lang.String" value="/data/jenkins" override="true"/>
</Context>
```

---

## 🐧 3.5 Installing Jenkins on Debian or Ubuntu

```bash
wget -q -O - http://pkg.jenkins-ci.org/debian/jenkins-ci.org.key | sudo apt-key add -
sudo sh -c 'echo deb http://pkg.jenkins-ci.org/debian binary/ > /etc/apt/sources.list.d/jenkins.list'
sudo aptitude update
sudo aptitude install -y jenkins
```

### Manage Jenkins service:
```bash
sudo /etc/init.d/jenkins start
sudo /etc/init.d/jenkins stop
```

---

## 🎩 3.6 Installing Jenkins on RedHat, Fedora, or CentOS

```bash
sudo wget -O /etc/yum.repos.d/jenkins.repo http://jenkins-ci.org/redhat/jenkins.repo
sudo rpm --import http://pkg.jenkins-ci.org/redhat/jenkins-ci.org.key
sudo yum install java-1.6.0-openjdk  # if needed
sudo yum install jenkins
sudo service jenkins start
```

---

## 🧊 3.7 Installing Jenkins on SUSE or OpenSUSE
> Use RedHat RPM instructions; dependencies may differ.

---

## ⚙️ 3.8 Running Jenkins as a Stand-Alone Application

```bash
java -jar jenkins.war
```

### Change default port:
```bash
java -jar jenkins.war --httpPort=8180
```

---

## 🌐 3.9 Running Jenkins Behind Apache

> Set up a reverse proxy using `mod_proxy`:
In Apache config:
```apache
ProxyPass /jenkins http://localhost:8080/jenkins
ProxyPassReverse /jenkins http://localhost:8080/jenkins
```

---

## 🧩 3.10 Running Jenkins on an Application Server

### Tomcat example:
Place `jenkins.war` in:
```
$CATALINA_HOME/webapps/
```

---

## 🧠 3.11 Memory Considerations

In `.profile`:
```bash
export JAVA_OPTS=-Djava.awt.headless=true -Xmx512m -DJENKINS_HOME=/data/jenkins
export MAVEN_OPTS="-Xmx512m -XX:MaxPermSize=256m"
export ANT_OPTS="-Xmx512m -XX:MaxPermSize=256m"
```

---

## 🪟 3.12 Installing Jenkins as a Windows Service
(Not applicable to Linux)

---

## 📁 3.13 What’s in the Jenkins Home Directory
- `.jenkins/` — main config
- `jobs/` — builds and configs
- `plugins/`, `users/`, `updates/` etc.

---

## 💾 3.14 Backing Up Your Jenkins Data
Just backup the entire `JENKINS_HOME` directory:
```bash
cp -r /var/lib/jenkins /backup/location/
```

---

## 🔄 3.15 Upgrading Your Jenkins Installation
1. Backup `JENKINS_HOME`
2. Download new `.war`
3. Replace the old `.war` and restart:
```bash
java -jar jenkins.war
```

---

## 🎉 3.16 Conclusion
> With Jenkins installed, you're ready to move on to configuration and job creation.

---
