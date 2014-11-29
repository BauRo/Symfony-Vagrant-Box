Symfony-Vagrant-Box
===================
A development vagrant box for Symfony projects.
All the tools you need are already pre-installed.

Configuration
-------------

Pre-installed packages:
  - apache2
  - php5
  - sendmail
  - unzip
  - git
  - vim
  - curl
  - acl
  - mysql-server
  - mysql-client
  - python-mysqldb
  - nodejs
  - npm
  
PHP Extensions:
  - php5-mysql
  - php-apc
  - php5-xmlrpc
  - php-soap
  - php5-gd
  - php5-pgsql
  - php5-curl
  - php5-cli
  - php5-xdebug
  
Node Modules:
  - karma
  - karma-mocha
  - chai
  - karma-phantomjs-launcher
  
Toolset
-------
- codeception: A tool for testing your code in php (unit, functional and acceptance)
- x-debug: A debug tool for PHP
- Mocha & Chai: code testing library for javascript completed with PhantomJS

PHP is fully installed together with a Mysql database

How to setup
------------

### Host configuration
The file 'shared-hosts.yml' inside the folder 'ansible/vars/' contains the configuration for the hostname of your website.
Below you see the default configuration.

```apache
    hostname: your-domain.com
        vhosts:
          'your-domain.com':
            enabled: true
            listen:
              - '*:80'
              - '127.0.0.1:8080'
            root: /storage/data/your-domain.com/web
            name: your-domain.com
            aliases:
              - www.your-domain.com
        #    settings:
```
 
### Server configuration
Inside the folder 'ansible/vars/dev' there are a couple config files. 
Here you can change the default setup.
For example inside the file 'install.yml' you can change the packages and extensions that are installed on your dev environment.

How to run
----------
On your computer you need to install a couple of programs.
- Vagrant: https://www.vagrantup.com/
- Ansible: http://docs.ansible.com/intro_installation.html
- Virtual box: https://www.virtualbox.org/wiki/Downloads

1. Inside your /etc/hosts file add the configured hostname and point it to ip 192.168.5.115
2. After you installed this tools you can run 'vagrant up' in a terminal app.
Be aware that you need to do this inside the dir where the file 'Vagrantfile' is located.
With this command the setup of your box is started. When the command is fully processed the dev enviroment is ready t use.
3. Add the ip 192.168.5.1 inside the file 'data/your-domain.com/web/app_dev.php' on line number 14
Like: 
```php
    '|| !in_array(@$_SERVER['REMOTE_ADDR'], array('127.0.0.1', 'fe80::1', '::1', '192.168.5.1'))'
```
4. When you go to http://yourcongiguredhostname/app_dev.php you see the Symfony demo app and you can start building your Symfony app.

Vagrant commands
----------------

vagrant up: start your development box
vagrant provision: run ansible configuarations on your box (needed after changing the configuaration files)
vagrant halt: power down the vagrant box
vagrant destroy: delete your vagrant box
