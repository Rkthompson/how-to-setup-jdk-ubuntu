# How to install and configure Java JDK on Ubuntu

## Summary
This doc covers the basic steps followed to get a working setup of the Java JDK that is recognized by VSCode on a Ubuntu dev box.

## Resources
[Oracle Java SE 11 (LTS)](https://www.oracle.com/java/technologies/javase-downloads.html)

## Steps
---
### Commands to run in the Linux terminal to check previous installs of Java.

To check what version of Java is currently installed and running:
```bash
java --version
```

To find the location of any previous JDK installs:
```bash
whereis java
```

Use ls -l to check where the symbolic link is pointing (assuming /usr/bin/java was returned by the whereis java command):
```bash
ls -l /usr/bin/java
```

Use ls -l to check where the next link is pointing (assuming /etc/alternatives/java  was returned by the previous command):
```bash
ls -l /etc/alternatives/java
```
What's returned is the actual location of Java on Ubuntu
In this example it's returned as:
```bash
lrwxrwxrwx 1 root root 33 Jun 19 10:21 /etc/alternatives/java -> /usr/lib/jvm/jdk-11.0.11/bin/java
```
/usr/lib/jvm/jdk-11.0.11/bin/java is the location of java displayed at the end of the string.

To uninstall a previously installed version of java along with its dependencies use:
```bash
sudo apt-get autoremove openjdk-11.jre
```
In this example the previous version was Open JDK version 11.  Replace openjdk-11 with the version you wish to uninstall.

### Download and install the new JDK

Download the newest LTS release from Orcale. [Oracle Java SE 11 (LTS)](https://www.oracle.com/java/technologies/javase-downloads.html)

From the command line (Assuming JDK is downloaded to /Downloads/ and jdk-11.0.11_linux-x64_bin.deb is the file downloaded):
```bash
sudo dpkg -i jdk-11.0.11_linux-x64_bin.deb
```

Update the alternatives for javac
```bash
sudo update-alternatives --install /usr/bin/javac javac /usr/lib/jvm/jdk-11.0.11/bin/javac 1
```

Check the install of javac
```bash
javac --version
```

update the alternatives for java
```bash
sudo update-alternatives --install /usr/bin/java java /usr/lib/jvm/jdk-11.0.11/bin/java 1
```
Check the install of java
```bash
java --version
```

Check the pathing to java:
```bash
sudo update-alternatives --config java
```

Setup the system path:
```bash
sudo nano /etc/environment
```
At the bottom of the file the following using the path returned from --config java:
```text
JAVA_HOME="/usr/lib/jvm/jdk-11.0.11"
```

Refresh for the updated path to take effect:
```bash
source /etc/environment
```

Double check the entry:
```bash
echo $JAVA_HOME
```
This should return the java home variable value (/usr/lib/jvm/jdk-11.0.11 in this example).

















