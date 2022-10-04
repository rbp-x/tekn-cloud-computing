## How to Uninstall and Installing Java JDK8 On Linux Ubuntu 22.04

## Uninstall

Launch the terminal using Ctrl + Alt + T. 

sudo apt remove default-jdk default-jre

Typing 'Y'

OpenJDK and OpenJRE will be automatically removed from your computer.

For those who have installed the Oracle JDK, there are two ways to uninstall Java. You can double-click on the .deb package file to open Software Center and then click on the Remove button to uninstall the package.

1. Open up the terminal on Ubuntu. 

2. Get the JDK package name using dpkg and grep.

dpkg --list | grep jdk


3. Uninstall the package using apt. Replace the package name with the output of the previous command.

sudo apt remove jdk[version]

Typing 'Y' and press enter!



## Install and Setup Java

Launch the terminal using Ctrl + Alt + T. 

1. sudo apt update
2. sudo apt install openjdk-8-jdk openjdk-8-jre
typing 'Y'
3. done

Next STEP Setup JAVA_HOME and JRE_HOME

first, check point Java :

1. sudo gedit /etc/environment
JAVA_HOME="/usr/lib/jvm/java-8-openjdk-amd64"
JRE_HOME="/usr/lib/jvm/java-8-openjdk-amd64/jre"

2. sudo apt-get update
3. Restart PC/Laptop

Next Download and Install Apache OfBiz !

1. create directory ofbiz on direcotry 'opt' use command : sudo mkdir ofbiz
2. wget https://dlcdn.apache.org/ofbiz/apache-ofbiz-18.12.05.zip

let’s extract a downloaded archive file.
3. sudo unzip apache-ofbiz-18.12.05.zip 
move to usr/local
4. sudo mv apache-ofbiz-18.12.05 /usr/local/apache-ofbiz
remove zip
5. sudo rm -f apache-ofbiz-18.12.05.zip

Install and conf environment status

1. sudo nano /etc/environment

PATH="/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:>
JAVA_HOME="/usr/lib/jvm/java-8-openjdk-amd64/jre/bin/"
JRE_HOME="/usr/lib/jvm/java-8-openjdk-amd64/jre/bin/"

2. Update
sudo update-alternatives --install "/usr/bin/java" "java" "/usr/lib/jvm/jdk1.8.0_341/bin/java" 0
sudo update-alternatives --install "/usr/bin/javac" "javac" "/usr/lib/jvm/jdk1.8.0_341/bin/javac" 0
sudo update-alternatives --set java /usr/lib/jvm/jdk1.8.0_341/bin/java
sudo update-alternatives --set javac /usr/lib/jvm/jdk1.8.0_341/bin/javac

update-alternatives --list java
update-alternatives --list javac

Download OfBiz
1. wget https://dlcdn.apache.org/ofbiz/apache-ofbiz-18.12.06.zip

sudo unzip apache-ofbiz-18.12.05.zip 
sudo mv apache-ofbiz-18.12.05 /usr/local/apache-ofbiz 
sudo rm -f apache-ofbiz-18.12.05.zip


Installing Apache Of-Biz with error gradle.wrapper

./gradlew loadDefault ofbiz [error]

Download Gradle package
Error Gradle with 
wget -c https://services.gradle.org/distributions/gradle-7.5.1-bin.zip

/opt/gradle/
sudo nano /etc/profile.d/gradle.sh   
  
export GRADLE_HOME=/opt/gradle/gradle-7.5.1
export PATH=${GRADLE_HOME}/bin:${PATH}

Change the permissions of file
sudo chmod +x /etc/profile.d/gradle.sh

Install the Gradle
Finally, load the environment variables using:

source /etc/profile.d/gradle.sh

gradle --version






sudo apt-get update






