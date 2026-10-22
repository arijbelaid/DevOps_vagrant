Vagrant.configure("2") do |config|
  # On utilise la même box que pour la démo
  config.vm.box = "bento/ubuntu-24.04"

  # ==========================================
  # MACHINE 1 : web1
  # ==========================================
  config.vm.define "web1" do |web1|
    web1.vm.hostname = "web1"
    
    # Réseau privé (permet aux VMs de se voir entre elles)
    web1.vm.network "private_network", ip: "192.168.56.10"
    
    # Redirection de ports (Hôte de la VM de lab -> VM Vagrant)
    web1.vm.network "forwarded_port", guest: 8082, host: 8082 # Site web
    web1.vm.network "forwarded_port", guest: 8081, host: 8081 # Jenkins
    web1.vm.network "forwarded_port", guest: 9000, host: 9000 # Portainer
    
    # Ressources allouées à la VM
    web1.vm.provider "virtualbox" do |vb|
      vb.name = "vagrant-web1"
      vb.memory = 2048
      vb.cpus = 2
    end

    # Provisionnement avec Ansible
    web1.vm.provision "ansible" do |ansible|
      ansible.playbook = "playbook.yml"
    end
  end

  # ==========================================
  # MACHINE 2 : web2
  # ==========================================
  config.vm.define "web2" do |web2|
    web2.vm.hostname = "web2"
    
    # Réseau privé (IP différente de web1)
    web2.vm.network "private_network", ip: "192.168.56.11"
    
    # Redirection de ports (on utilise des ports hôtes différents pour éviter les conflits avec web1)
    web2.vm.network "forwarded_port", guest: 8082, host: 18082 # Site web (port hôte 18082)
    web2.vm.network "forwarded_port", guest: 8081, host: 18081 # Jenkins (port hôte 18081)
    web2.vm.network "forwarded_port", guest: 9000, host: 19000 # Portainer (port hôte 19000)
    
    # Ressources allouées à la VM
    web2.vm.provider "virtualbox" do |vb|
      vb.name = "vagrant-web2"
      vb.memory = 2048
      vb.cpus = 2
    end

    # Provisionnement avec Ansible
    web2.vm.provision "ansible" do |ansible|
      ansible.playbook = "playbook.yml"
    end
  end
end
