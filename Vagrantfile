#! TP2 - DevOps - Virtualisation - Linux

Vagrant.configure("2") do |config|

  config.vm.box = "bento/ubuntu-22.04"
  config.vm.box_check_update = false

  # VM srv-app
  config.vm.define "srv-app" do |srv|
    srv.vm.hostname = "srv-app"
    srv.vm.network "private_network", ip: "192.168.0.11"
    srv.vm.network "forwarded_port", guest: 8080, host: 8080

    srv.vm.provider "virtualbox" do |vb|
      vb.name = "srv-app"
      vb.memory = 1024
      vb.cpus = 1
    end

    srv.vm.provision "shell", inline: <<-SHELL
      apt-get update -y

      # Java 17
      apt-get install -y openjdk-17-jdk

      java -version

      # Tomcat 9
      apt-get install -y tomcat9 tomcat9-admin

      systemctl enable tomcat9
      systemctl start tomcat9

      # Permissions correctes
      chown -R tomcat:tomcat /var/lib/tomcat9

      echo "Provisioning terminé"
    SHELL
  end

  # VM srv-db
  config.vm.define "srv-db" do |srv|
    srv.vm.hostname = "srv-db"
    srv.vm.network "private_network", ip: "192.168.0.12"

    srv.vm.provider "virtualbox" do |vb|
      vb.name = "srv-db"
      vb.memory = 1024
      vb.cpus = 1
    end

    srv.vm.provision "shell", inline: <<-SHELL
      apt update -y
    SHELL
  end

end
