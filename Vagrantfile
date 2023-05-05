
#################### JENKINS VM #######################
# http://192.168.56.140:8080/ to login

Vagrant.configure("2") do |config|
  config.vm.provision "shell", inline: "echo Hello"

  config.vm.define "jenkins" do |jenkins|
    jenkins.vm.box = "generic/ubuntu1804"
    jenkins.vm.network "private_network", ip: "192.168.56.140"
    jenkins.vm.synced_folder "D:\\shells_scripts", "/vagrant_data"
    jenkins.vm.provider "virtualbox" do |vb|
        vb.memory = 2048
        vb.cpus = 2
    end
    jenkins.vm.provision "shell", inline: <<-SHELL
    sudo apt update
sudo apt install openjdk-11-jdk -y
sudo apt install maven -y
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null
echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
sudo apt-get update
sudo apt-get install jenkins -y
  SHELL
  end

######################### SONAR VM ####################
#login http://http//192.168.56.141:9000
#config script: /opt/scripts/config.sh

  config.vm.define "sonar" do |sonar|
    sonar.vm.box = "generic/ubuntu1804"
    sonar.vm.network "private_network", ip: "192.168.56.141"
    sonar.vm.synced_folder "D:\\shells_scripts", "/vagrant_data"
    sonar.vm.provider "virtualbox" do |vb|
      vb.memory = 1024
      vb.cpus = 2
  end
#  sonar.vm.provision "shell", inline: <<-SHELL
#  SHELL
end

##################### NEXUS VM #######################

config.vm.define "nexus" do |nexus|
  nexus.vm.box = "geerlingguy/centos7"
  nexus.vm.network "private_network", ip: "192.168.56.142"
  nexus.vm.synced_folder "D:\\shells_scripts", "/vagrant_data"
  nexus.vm.provider "virtualbox" do |vb|
    vb.memory = 1024
    vb.cpus = 2
end
nexus.vm.provision "shell", inline: <<-SHELL
yum install java-1.8.0-openjdk.x86_64 wget -y   
mkdir -p /opt/nexus/   
mkdir -p /tmp/nexus/                           
cd /tmp/nexus/
NEXUSURL="https://download.sonatype.com/nexus/3/latest-unix.tar.gz"
wget $NEXUSURL -O nexus.tar.gz
EXTOUT=`tar xzvf nexus.tar.gz`
NEXUSDIR=`echo $EXTOUT | cut -d '/' -f1`
rm -rf /tmp/nexus/nexus.tar.gz
rsync -avzh /tmp/nexus/ /opt/nexus/
useradd nexus
chown -R nexus.nexus /opt/nexus 
cat <<EOT>> /etc/systemd/system/nexus.service
[Unit]                                                                          
Description=nexus service                                                       
After=network.target                                                            
                                                                  
[Service]                                                                       
Type=forking                                                                    
LimitNOFILE=65536                                                               
ExecStart=/opt/nexus/$NEXUSDIR/bin/nexus start                                  
ExecStop=/opt/nexus/$NEXUSDIR/bin/nexus stop                                    
User=nexus                                                                      
Restart=on-abort                                                                
                                                                  
[Install]                                                                       
WantedBy=multi-user.target                                                      
EOT
echo 'run_as_user="nexus"' > /opt/nexus/$NEXUSDIR/bin/nexus.rc
systemctl daemon-reload
systemctl start nexus
systemctl enable nexus
SHELL
end

end