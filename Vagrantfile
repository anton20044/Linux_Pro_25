# -*- mode: ruby -*-
# vim: set ft=ruby :

MACHINES = {
  :inetRouter => {
        :box_name => "centos8",
        :box_version => "0",
        :vm_name => "inetRouter",
  },
  :centralRouter => {
        :box_name => "centos8",
        :box_version => "0",
        :vm_name => "centralRouter",
  },

  :office1Router => {
        :box_name => "centos8",
        :box_version => "0",
        :vm_name => "office1Router",
  },

  :testClient1 => {
        :box_name => "centos8",
        :box_version => "0",
        :vm_name => "testClient1",
  },

  :testServer1 => {
        :box_name => "centos8",
        :box_version => "0",
        :vm_name => "testServer1",
  },

  :testClient2 => {
        :box_name => "ubuntu/jammy64",
        :box_version => "0",
        :vm_name => "testClient2",
  },

  :testServer2 => {
        :box_name => "ubuntu/jammy64",
        :box_version => "0",
        :vm_name => "testServer2",
  },

}

Vagrant.configure("2") do |config|

  MACHINES.each do |boxname, boxconfig|
    
    config.vm.define boxname do |box|
   
      box.vm.box = boxconfig[:box_name]
      box.vm.host_name = boxconfig[:vm_name]
      box.vm.box_version = boxconfig[:box_version]

      config.vm.provider "virtualbox" do |v|
        v.memory = 1024
        v.cpus = 2
       end

      if boxconfig[:vm_name] == "inetRouter"
        box.vm.network "private_network", adapter: 2, auto_config: false, virtualbox__intnet: "router-net"
        box.vm.network "private_network", adapter: 3, auto_config: false, virtualbox__intnet: "router-net"
        box.vm.network "private_network", ip: '192.168.56.100', adapter: 8
        box.vm.provision "shell", inline: <<-SHELL
          sudo sed -i 's/mirrorlist/#mirrorlist/g' /etc/yum.repos.d/CentOS-*
          sudo sed -i 's|#baseurl=http://mirror.centos.org|baseurl=http://vault.centos.org|g' /etc/yum.repos.d/CentOS-*
          mkdir -p ~root/.ssh
          cp ~vagrant/.ssh/auth* ~root/.ssh
          sed -i 's/^PasswordAuthentication.*$/PasswordAuthentication yes/' /etc/ssh/sshd_config
          systemctl restart sshd.service
        SHELL

      end


      if boxconfig[:vm_name] == "centralRouter"
        box.vm.network "private_network", adapter: 2, auto_config: false, virtualbox__intnet: "router-net"
        box.vm.network "private_network", adapter: 3, auto_config: false, virtualbox__intnet: "router-net"
        box.vm.network "private_network", ip: '192.168.255.9', adapter: 6, netmask: "255.255.255.252", virtualbox__intnet: "office1-central"
        box.vm.network "private_network", ip: '192.168.56.110', adapter: 8
        box.vm.provision "shell", inline: <<-SHELL
          sudo sed -i 's/mirrorlist/#mirrorlist/g' /etc/yum.repos.d/CentOS-*
          sudo sed -i 's|#baseurl=http://mirror.centos.org|baseurl=http://vault.centos.org|g' /etc/yum.repos.d/CentOS-*
          mkdir -p ~root/.ssh
          cp ~vagrant/.ssh/auth* ~root/.ssh
          sed -i 's/^PasswordAuthentication.*$/PasswordAuthentication yes/' /etc/ssh/sshd_config
          systemctl restart sshd.service
        SHELL

      end


      if boxconfig[:vm_name] == "office1Router"
        box.vm.network "private_network", ip: '192.168.255.10', adapter: 2, netmask: "255.255.255.252", virtualbox__intnet: "office1-central"
        box.vm.network "private_network", adapter: 3, auto_config: false, virtualbox__intnet: "vlan1"
        box.vm.network "private_network", adapter: 4, auto_config: false, virtualbox__intnet: "vlan1"
        box.vm.network "private_network", adapter: 5, auto_config: false, virtualbox__intnet: "vlan2"
        box.vm.network "private_network", adapter: 6, auto_config: false, virtualbox__intnet: "vlan2"
        box.vm.network "private_network", ip: '192.168.56.200', adapter: 8
        box.vm.provision "shell", inline: <<-SHELL
          sudo sed -i 's/mirrorlist/#mirrorlist/g' /etc/yum.repos.d/CentOS-*
          sudo sed -i 's|#baseurl=http://mirror.centos.org|baseurl=http://vault.centos.org|g' /etc/yum.repos.d/CentOS-*
          mkdir -p ~root/.ssh
          cp ~vagrant/.ssh/auth* ~root/.ssh
          sed -i 's/^PasswordAuthentication.*$/PasswordAuthentication yes/' /etc/ssh/sshd_config
          systemctl restart sshd.service
        SHELL

      end

      if boxconfig[:vm_name] == "testClient1"
        box.vm.network "private_network", adapter: 2, auto_config: false, virtualbox__intnet: "testLAN"
        box.vm.network "private_network", ip: '192.168.56.210', adapter: 8
        box.vm.provision "shell", inline: <<-SHELL
          sudo sed -i 's/mirrorlist/#mirrorlist/g' /etc/yum.repos.d/CentOS-*
          sudo sed -i 's|#baseurl=http://mirror.centos.org|baseurl=http://vault.centos.org|g' /etc/yum.repos.d/CentOS-*
          mkdir -p ~root/.ssh
          cp ~vagrant/.ssh/auth* ~root/.ssh
          sed -i 's/^PasswordAuthentication.*$/PasswordAuthentication yes/' /etc/ssh/sshd_config
          systemctl restart sshd.service
        SHELL

      end

      if boxconfig[:vm_name] == "testServer1"
        box.vm.network "private_network", adapter: 2, auto_config: false, virtualbox__intnet: "testLAN"
        box.vm.network "private_network", ip: '192.168.56.220', adapter: 8
        box.vm.provision "shell", inline: <<-SHELL
          sudo sed -i 's/mirrorlist/#mirrorlist/g' /etc/yum.repos.d/CentOS-*
          sudo sed -i 's|#baseurl=http://mirror.centos.org|baseurl=http://vault.centos.org|g' /etc/yum.repos.d/CentOS-*
          mkdir -p ~root/.ssh
          cp ~vagrant/.ssh/auth* ~root/.ssh
          sed -i 's/^PasswordAuthentication.*$/PasswordAuthentication yes/' /etc/ssh/sshd_config
          systemctl restart sshd.service
        SHELL
      end

      if boxconfig[:vm_name] == "testClient2"
        box.vm.network "private_network", adapter: 2, auto_config: false, virtualbox__intnet: "testLAN"
        box.vm.network "private_network", ip: '192.168.56.230', adapter: 8
        box.vm.provision "shell", inline: <<-SHELL
          mkdir -p ~root/.ssh
          cp ~vagrant/.ssh/auth* ~root/.ssh
          sed -i 's/^PasswordAuthentication.*$/PasswordAuthentication yes/' /etc/ssh/sshd_config.d/60-cloudimg-settings.conf
          systemctl restart sshd.service
        SHELL
      end

      if boxconfig[:vm_name] == "testServer2"
        box.vm.network "private_network", adapter: 2, auto_config: false, virtualbox__intnet: "testLAN"
        box.vm.network "private_network", ip: '192.168.56.240', adapter: 8
        box.vm.provision "shell", inline: <<-SHELL
          mkdir -p ~root/.ssh
          cp ~vagrant/.ssh/auth* ~root/.ssh
          sed -i 's/^PasswordAuthentication.*$/PasswordAuthentication yes/' /etc/ssh/sshd_config.d/60-cloudimg-settings.conf
          systemctl restart sshd.service
        SHELL

      end

      if boxconfig[:vm_name] == "testServer2"
       box.vm.provision "ansible" do |ansible|
        ansible.playbook = "ansible/provision.yml"
        ansible.inventory_path = "ansible/hosts"
        ansible.host_key_checking = "false"
        ansible.limit = "all"
       end
      end



    end
  end
end
