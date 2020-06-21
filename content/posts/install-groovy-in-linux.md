---
title: "Install groovy in linuxmint"
date: 2020-05-30T18:19:08+05:30
draft: false
authors: ["anbuchelva"]
resources:
- name: "featured-image"
  src: "https://upload.wikimedia.org/wikipedia/commons/thumb/3/36/Groovy-logo.svg/1280px-Groovy-logo.svg.png"
toc: false
---
I use Linux Mint distro in my primary machine; the steps are given below to install groovy on the machine.

# Download & Install
Steps to install groovy in Linux  
```
curl -s get.sdkman.io | bash
source "$HOME/.sdkman/bin/sdkman-init.sh"
sdk install groovy
groovy -version
```

# Check Java Version & Configure

Check Java version in terminal by typing `java -version`

this should return the result as following:
```
openjdk version "1.8.0_252"
OpenJDK Runtime Environment (build 1.8.0_252-8u252-b09-1~18.04-b09)
OpenJDK 64-Bit Server VM (build 25.252-b09, mixed mode)
````

Groovy doesn't support the latest versions as of today (24th May 2020) it supports only upto Java-8.  If new versions are installed it has to be downgraded to Java 8.

If you have a latest version download Java 8.
```
sudo apt-get install openjdk-8-jre
```
Then
```
sudo update-alternatives --config java
```
the result might look like this:
```
There are 2 choices for the alternative java (providing /usr/bin/java).

  Selection    Path                                            Priority   Status
------------------------------------------------------------
* 0            /usr/lib/jvm/java-11-openjdk-amd64/bin/java      1111      auto mode
  1            /usr/lib/jvm/java-11-openjdk-amd64/bin/java      1111      manual mode
  2            /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java   1081      manual mode

Press <enter> to keep the current choice[*], or type selection number: 
```
choose the option 2 (or whichever points to Java8).  Now check the `java -version` again.

once it is configured check wither the `JAVA_HOME` is configured by `echo $JAVA_HOME`.  It should give the output something link this.
```
/usr/lib/jvm/java-1.8.0-openjdk-amd64
```

If you are not seeing it, you need to modify something as per the below steps.
create a file `jdk.sh` in the path by `sudo touch /etc/profile.d/jdk.sh`. Then open the file with elevated permission (sudo).

you may use any of your favourite text editors. I used xed in Linux Mint
```
sudo xed /etc/profile.d/jdk.sh
```
Paste the following in the file and save it. The JAVA_HOME line should represent where the Java8 is installed.
```
JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-amd64
PATH=$PATH:$HOME/bin:$JAVA_HOME/bin
export JAVA_HOME
export JRE_HOME
export PATH
```
once you close the text editor give execute permission to the file `sudo chmod +x /etc/profile.d/jdk.sh`.  Then close all applications and logout and login back.

Check `echo $JAVA_HOME`. You should be seeing the java home.

# Run Groovy

command to run groovy within the terminal
```
groovysh
```
command to trigger groovy terminal
```
groovyConsole
```
To run a specific Groovy script type:
```
groovy SomeScriptName
``` 

