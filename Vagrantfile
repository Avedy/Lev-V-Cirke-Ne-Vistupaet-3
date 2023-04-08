# -*- mode: ruby -*-
# vim: set ft=ruby :

MACHINES = {
  :web1 => {
        :box_name => "redos732",
        :ip_addr => '192.168.11.111'
  },
  :web2 => {
        :box_name => "redos732",
        :ip_addr => '192.168.11.112'
  },
  :rrobin => {
        :box_name => "redos732",
        :ip_addr => '192.168.11.113'
  }
}

Vagrant.configure("2") do |config|
  MACHINES.each do |boxname, boxconfig|
      config.vm.define boxname do |box|
          box.vm.box = boxconfig[:box_name]
          box.vm.host_name = boxname.to_s
          box.vm.network "private_network", ip: boxconfig[:ip_addr]
          box.vm.provider :virtualbox do |vb|
            vb.customize ["modifyvm", :id, "--memory", "512"]
          end
          config.vm.provision "shell" do |s|
			ssh_pub_key = File.readlines("/home/avedy/.ssh/id_rsa.pub").first.strip
			s.inline = <<-SHELL
			mkdir -p /home/vagrant/.ssh
			sudo mkdir -p /root/.ssh
			echo #{ssh_pub_key} >> /home/vagrant/.ssh/authorized_keys
			echo #{ssh_pub_key} >> /root/.ssh/authorized_keys
            sed -i '65s/PasswordAuthentication no/PasswordAuthentication yes/g' /etc/ssh/sshd_config
            systemctl restart sshd
			SHELL
		  end
      end
  end
end
