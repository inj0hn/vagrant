sudo apt-get update -y
sudo apt-get upgrade -y

-- install java 8
wget https://cdn.azul.com/zulu/bin/zulu8.36.0.1-ca-jdk8.0.202-linux_x64.tar.gz -P ~/Downloads

mkdir /usr/lib/jvm
cp ~/Downloads/zulu8.36.0.1-ca-jdk8.0.202-linux_x64.tar.gz /usr/lib/jvm/
cd /usr/lib/jvm/
sudo tar -xzvf zulu8.36.0.1-ca-jdk8.0.202-linux_x64.tar.gz
sudo rm zulu8.36.0.1-ca-jdk8.0.202-linux_x64.tar.gz

sudo gedit /etc/profile.d/javaenv.sh
-- TODO add the following to javaenv.sh
export JAVA_HOME=/usr/lib/jvm/zulu8.36.0.1-ca-jdk8.0.202-linux_x64
export PATH=${JAVA_HOME}/bin:$PATH

sudo chmod +x /etc/profile.d/javaenv.sh
sudo source /etc/profile.d/javaenv.sh

-- install maven
cd /opt
sudo wget http://www-eu.apache.org/dist/maven/maven-3/3.3.9/binaries/apache-maven-3.3.9-bin.tar.gz
sudo tar -xvzf apache-maven-3.3.9-bin.tar.gz
sudo mv apache-maven-3.3.9 maven
sudo rm apache-maven-3.3.9-bin.tar.gz

sudo gedit /etc/profile.d/mavenenv.sh
-- TODO add the following to mavenenv.sh
export M2_HOME=/opt/maven
export PATH=${M2_HOME}/bin:$PATH

sudo chmod +x /etc/profile.d/mavenenv.sh
sudo source /etc/profile.d/mavenenv.sh

-- install git
sudo apt-get install git-core -y

