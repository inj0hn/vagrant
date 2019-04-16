$script = <<-SCRIPT
echo provisioning machine...
sudo apt-get update -y
sudo apt-get upgrade -y
sudo apt-get install curl -y

echo installing jdk8...
wget --no-cookies --no-check-certificate --header \
"Cookie: gpw_e24=http%3a%2F%2Fwww.oracle.com%2Ftechnetwork%2Fjava%2Fjavase%2Fdownloads%2Fjdk8-downloads-2133151.html; oraclelicense=accept-securebackup-cookie;" \
"https://download.oracle.com/otn-pub/java/jdk/8u201-b09/42970487e3af4f5aa5bca3f542482c60/jdk-8u201-linux-x64.tar.gz"
mkdir /usr/lib/jvm
sudo mv jdk-8u201-linux-x64.tar.gz /usr/lib/jvm
cd /usr/lib/jvm
sudo tar -xzvf jdk-8u201-linux-x64.tar.gz && sudo rm jdk-8u201-linux-x64.tar.gz
cd ~ && sudo touch /etc/profile.d/javaenv.sh && sudo chown vagrant /etc/profile.d/javaenv.sh && sudo chmod +x /etc/profile.d/javaenv.sh
echo 'export JAVA_HOME=/usr/lib/jvm/jdk1.8.0_201' >> /etc/profile.d/javaenv.sh
echo 'export PATH=${JAVA_HOME}/bin:$PATH' >> /etc/profile.d/javaenv.sh
source /etc/profile.d/javaenv.sh

echo installing jce...
wget --no-check-certificate --no-cookies --header \
"Cookie: oraclelicense=accept-securebackup-cookie" \
"http://download.oracle.com/otn-pub/java/jce/8/jce_policy-8.zip
unzip jce_policy-8.zip && rm jce_policy-8.zip
sudo mv UnlimitedJCEPolicyJDK8/local_policy.jar /usr/lib/jvm/jdk1.8.0_201/jre/lib/security/
sudo mv UnlimitedJCEPolicyJDK8/US_export_policy.jar /usr/lib/jvm/jdk1.8.0_201/jre/lib/security/
rm -r UnlimitedJCEPolicyJDK8/

echo installing maven...
cd /opt
sudo wget http://www-eu.apache.org/dist/maven/maven-3/3.3.9/binaries/apache-maven-3.3.9-bin.tar.gz
sudo tar -xvzf apache-maven-3.3.9-bin.tar.gz && sudo rm apache-maven-3.3.9-bin.tar.gz
sudo touch /etc/profile.d/mavenenv.sh && sudo chown vagrant /etc/profile.d/mavenenv.sh && sudo chmod +x /etc/profile.d/mavenenv.sh
echo 'export M2_HOME=/opt/apache-maven-3.3.9' >> /etc/profile.d/mavenenv.sh
echo 'export PATH=${M2_HOME}/bin:$PATH' >> /etc/profile.d/mavenenv.sh
source /etc/profile.d/mavenenv.sh

echo installing git...
sudo apt-get install git-core -y

echo installing msysql...
sudo apt install mysql-server -y

echo installing redis...
sudo apt-get install redis-server -y
sudo systemctl enable redis-server.service

echo installing terminator...
sudo apt-get install terminator -y

echo installing brave...
curl -s https://brave-browser-apt-release.s3.brave.com/brave-core.asc | sudo apt-key --keyring /etc/apt/trusted.gpg.d/brave-browser-release.gpg add -
source /etc/os-release
echo "deb [arch=amd64] https://brave-browser-apt-release.s3.brave.com/ $UBUNTU_CODENAME main" | sudo tee /etc/apt/sources.list.d/brave-browser-release-${UBUNTU_CODENAME}.list
sudo apt install brave-keyring brave-browser -y
SCRIPT

Vagrant.configure("2") do |config|
  config.vm.provider "virtualbox" do |v|
    v.memory = 4096
    v.cpus = 2
  end
  config.vm.box = "bento/ubuntu-18.04"
  config.vm.provision "shell", inline: $script
end
