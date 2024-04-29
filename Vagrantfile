Vagrant.configure("2") do |config|
    config.vm.define "dev" do |dev|
      dev.vm.box = "gusztavvargadr/ubuntu-server-2204-lts"    

      dev.vm.network "forwarded_port", guest: 8080, host: 8080
      
      dev.vm.provider "virtualbox" do |vb|
        vb.memory = 2048
        vb.cpus = 2
	    vb.customize ["modifyvm", :id, "--audio", "none"] 
      end
      
      config.vm.provision "shell", privileged: false, inline: <<-SHELL

        sudo apt update
        sudo apt install fontconfig openjdk-17-jre -y

        sudo wget -O /usr/share/keyrings/jenkins-keyring.asc https://pkg.jenkins.io/debian/jenkins.io-2023.key

        echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
          https://pkg.jenkins.io/debian binary/ | sudo tee \
          /etc/apt/sources.list.d/jenkins.list > /dev/null

        sudo apt update
        sudo apt install jenkins -y
        
        sudo rm -f /etc/sudoers.d/jenkins
        sudo touch /etc/sudoers.d/jenkins
 
        sudo echo "# User rules for jenkins"        | sudo tee -a /etc/sudoers.d/jenkins 
        sudo echo "jenkins ALL=(ALL) NOPASSWD:ALL"  | sudo tee -a /etc/sudoers.d/jenkins

        sudo systemctl restart jenkins

        sudo cat /var/lib/jenkins/secrets/initialAdminPassword
        # http://localhost:8080

      SHELL
    end
end
