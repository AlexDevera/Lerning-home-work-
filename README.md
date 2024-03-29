```text
🎓 Lesson#1
--Target--
1)Writing a configuration file.
2) Verification of functionality.
3) Installing Ubuntu OS kernel updates.

```
--Vagrantfile example--
```ruby
ENV['VAGRANT_SERVER_URL'] = 'https://vagrant.elab.pro' # custum vagrant server whit OS images
Vagrant.configure("2") do |config| 
config.vm.box = "ubuntu/focal64" # Target OS
  config.vm.hostname = "lesson1" # Hostname VM
  config.vm.provider "virtualbox" do |vb| # Target hypervisor
    vb.memory = 4096 #Allocated memory
    vb.cpus = 4 # allocated CPU cores
  end # end VM configuration
  config.vm.network "private_network", ip: "192.168.56.12" # creating network interface whit ip address
  	config.vm.provision "shell", inline: <<-SHELL # do shell commands
    sudo apt-get update ; sudo apt upgrade -y ; sudo apt autoremove -y && sudo reboot   # shell commands (system update\upgrade)
  SHELL
end # finish 
```

```text
🎓 Lesson#2
!! Vagrantfile has been updated
--Target--
1) Write Vagrant File and playbook file
2) Autostart "Nginx" service after OS launch on 8080 port


```
--Playbook file example--

```yaml
- hosts: localhost
  become: true
  tasks:
    - name: Update apt cache
      apt:
        update_cache: yes

    - name: Install nginx
      apt:
        name: nginx
        state: present

    - name: Start nginx
      service:
        name: nginx
        state: started
        enabled: true
```
