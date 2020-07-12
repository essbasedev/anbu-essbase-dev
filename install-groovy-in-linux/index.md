# Install Groovy in Linux

I use Linux Mint distro in my primary machine; the steps are given below to install groovy on that machine.  The steps are similar to the one explained here, which may have slight difference compare to the steps explained here.  

<!--more-->

## Requirements

1. You will need elevated rights equal to root.
2. Java Development Kit is needed for executing groovy scripts _(if it is not installed already)_

## Download & Install groovy
Installing groovy using [sdkman](https://sdkman.io) is the easiest option.  Install sdkman as per the steps given below.   

```shell
curl -s get.sdkman.io | bash
source "$HOME/.sdkman/bin/sdkman-init.sh"
sdk install groovy
groovy -version
```

If JDK is not installed `groovy -version` would give error.

## Check Java Version & Configure

{{< admonition type=info title="Information" open=true >}}
This step is optional.  This is to be followed if JDK is not installed already.
{{< /admonition >}}

Check Java version in terminal by typing `java -version`.  You will get an error message, if Java is not installed already.  

To install __Java Development Kit__ type the following in terminal

```shell
sudo apt-get install openjdk-8-jre
```

if Java is already installed, you will get the output something like this  
```shell
openjdk version "11.0.7" 2020-04-14
OpenJDK Runtime Environment (build 11.0.7+10-post-Ubuntu-3ubuntu1)
OpenJDK 64-Bit Server VM (build 11.0.7+10-post-Ubuntu-3ubuntu1, mixed mode, sharing)
```

You need to know the installed path of Java and the versions installed.  Type the following command to know those.  

```shell
sudo update-alternatives --config java
```
the result might look like this if you have more than one version, in such case you need to select the compatible version of JDK.  
```shell
There are 2 choices for the alternative java (providing /usr/bin/java).

  Selection    Path                                            Priority   Status
------------------------------------------------------------
* 0            /usr/lib/jvm/java-11-openjdk-amd64/bin/java      1111      auto mode
  1            /usr/lib/jvm/java-11-openjdk-amd64/bin/java      1111      manual mode
  2            /usr/lib/jvm/java-8-openjdk-amd64/jre/bin/java   1081      manual mode

Press <enter> to keep the current choice[*], or type selection number: 
```
if you have only one version of Java Installed, you will get the following message.
```shell
There is only one alternative in link group java (providing /usr/bin/java): /usr/lib/jvm/java-11-openjdk-amd64/bin/java
Nothing to configure.
```
You will get to know the Java installed path from the above step.  

## Configure `$JAVA_HOME` path

The `$JAVA_HOME` path to be loaded when an user login to the system. So, create a file `jdk.sh` in the path by `sudo touch /etc/profile.d/jdk.sh`. Then open the file with elevated permission (sudo).

you may use any of your favourite text editors. I used xed in Linux Mint.  
```shell
sudo xed /etc/profile.d/jdk.sh
```
Paste the following in the file and save it. The JAVA_HOME line should represent where the Java is installed.
```shell
JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64
PATH=$PATH:$HOME/bin:$JAVA_HOME/bin
export JAVA_HOME
export JRE_HOME
export PATH
```
{{< admonition type=note title="Note" open=true >}}
The `$JAVA_HOME` path should be equal to the path where Java is installed, the same that you got to know in the previous step.  
{{< /admonition >}}

Close the text editor and give execute permission to the file by `sudo chmod +x /etc/profile.d/jdk.sh`.  Then close all applications and __logout__ and __login__ back.

Check `echo $JAVA_HOME`. You should be seeing the java home.

## Run Groovy

command to run groovy within the terminal
```shell
groovysh
```
command to trigger groovy terminal
```shell
groovyConsole
```shell
To run a specific Groovy script type:
```
groovy filename.groovy
```
leave your comment if you have any doubts.

