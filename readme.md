# Bootstrap64
Virtual Machine created for the PHP Bootcamp.

### Prerequisites
Install [Git](https://git-scm.com/downloads)  
Install [Vagrant](https://www.vagrantup.com/downloads.html)  
Install [VirtualBox](https://www.virtualbox.org/wiki/Downloads)  

### Windows prerequisites
You may need to enable hardware virtualization (VT-x). It can usually be enabled via your BIOS. If you are using [Hyper-V](https://docs.microsoft.com/en-us/virtualization/hyper-v-on-windows/quick-start/enable-hyper-v) on a UEFI system you may additionally need to disable Hyper-V in order to access VT-x.

Install the WinNFSd vagrant plugin
```bash
vagrant plugin install vagrant-winnfsd
```

### Setup

Install the VM
```bash
git clone git@github.com:desveladisimos/Bootcamp64.git ~/Bootcamp64
```

Boot the VM
```bash
cd ~/Bootcamp64 && vagrant up
```

Open the [browser](http://192.168.33.10)

### Database connection

Connection Method: Standard TCP/IP over SSH

SSH Hostname: 192.168.33.10  
SSH Username: vagrant  
SSH Password: vagrant  
SSH Key File: ~/Bootcamp64/.vagrant/machines/default/virtualbox/private_key  

MySQL Host: 127.0.0.1  
MySQL Port: 3306  
MySQL User: arkus  
MySQL Pass: nexus  

