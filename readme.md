# Bootstrap64
Virtual Machine created for the PHP Bootcamp.

### Prerequisites
Install [Git](https://git-scm.com/downloads)  
Install [Vagrant](https://www.vagrantup.com/downloads.html)  
Install [VirtualBox](https://www.virtualbox.org/wiki/Downloads)  
Install [MySQL Workbench](https://dev.mysql.com/downloads/workbench)  

### Installation

Clone the VM repository
```bash
git clone git@github.com:desveladisimos/Bootcamp64.git ~/Bootcamp64
```

Boot the VM
```bash
cd ~/Bootcamp64 && vagrant up
```

Load the Apache default page in the [browser](http://192.168.66.10)

### MySQL Workbench Connection Settings

Connection Method: Standard TCP/IP over SSH

```
SSH Hostname: 192.168.66.10  
SSH Username: vagrant  
SSH Password: vagrant  
SSH Key File: ~/Bootcamp64/.vagrant/machines/default/virtualbox/private_key  
```

```
MySQL Host: 127.0.0.1  
MySQL Port: 3306  
MySQL User: arkus  
MySQL Pass: nexus  
```

### Vagrant commands

The following table contains the basic vagrant commands.

Command | Description
--- | ---
```vagrant up``` | Boot the VM
```vagrant ssh``` | Log into the VM
```vagrant reload``` | Reload the VM
```vagrant halt``` | Shutdown the VM
```vagrant destroy``` | Destroy the VM

### Creating a laravel app

Let's say we are building a Laravel app called **todos**

Register the app domain in your hosts file
```bash
192.168.66.10  todos.local
```

- [Windows](https://www.google.com/search?q=windows+10+edit+hosts+file&oq=windows+10+edit+host&aqs=chrome.0.0j69i57j0j69i60j69i61l2.3419j0j4&sourceid=chrome&ie=UTF-8): ```c:\Windows\System32\Drivers\etc\hosts```
- [Linux or Mac](https://www.google.com/search?q=ubuntu+edit+hosts+file&oq=ubuntu+edit+hosts&aqs=chrome.0.0j69i57j0l4.7783j0j7&sourceid=chrome&ie=UTF-8): ```/etc/hosts```

SSH into the VM
```bash
cd ~/Bootcamp64 && vagrant ssh
```

Log into MySQL
```bash
mysql -u arkus -p
```

Create the database
```bash
create database todos;
```

Logout from MySQL
```bash
exit;
```

Go to the www directory
```bash
cd /var/www
```

Create the app
```bash
composer create-project laravel/laravel todos --prefer-dist
```

Move into the app
```bash
cd todos
```

Edit the database credentials listed in the .env file
```bash
DB_DATABASE=todos
DB_USERNAME=arkus
DB_PASSWORD=nexus
```

Migrate the database
```bash
php artisan migrate
```

Create the Apache Virtual Host
```bash
sudo virtualhost create todos.local /var/www/todos/public
```

Load the app in the [browser](http://todos.local)
