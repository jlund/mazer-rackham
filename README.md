mazer-rackham
=============

 Sample [Ansible](http://www.ansibleworks.com/) Playbook for Rack applications that installs Nginx, Passenger, Ruby 1.9.3 + the [Falcon patch](https://gist.github.com/funny-falcon/4755042). It also demonstrates how to deploy a [sample Rack application](https://github.com/jlund/imgur-display) using git.

 Specifically, it does the following:

 * Installs a few crucial packages like git and NTP
 * Creates a deploy user that the application files will belong to
 * Adds an SSH public key to the deploy user's Authorized Keys file
 * Reconfigures OpenSSH to only allow access via SSH keys
 * Installs Ruby 1.9.3 + the Falcon patch
 * Installs Bundler
 * Installs Nginx + Passenger
 * Sets up and enables an Nginx vhost
 * Creates all necessary application directories
 * Uses git to checkout the latest revision of the [imgur-display](https://github.com/jlund/imgur-display) codebase
 * Creates required symlinks
 * Uses bundler to install all Gem dependencies

Running this playbook will leave you with a fully-functional Rack application server that is ready to show you a random picture from imgur. With some incredibly minor adjustments, this playbook will deploy your own application! It's my hope that this will be helpful to anyone who needs to set up a similar server using Ansible.

This playbook was tested on Ubuntu 12.04.2 LTS but should also work on Debian 7.

Enjoy!

Testing this playbook with Vagrant
----------------------------------

* Install Ansible (this playbook requires version >1.2, which for now means you need the development version) 
* Download and install [Vagrant](http://vagrantup.com/)
* Copy or rename `Vagrantfile.example` to `Vagrantfile`
* Copy or rename `ansible_hosts.example` to `ansible_hosts`
* Comment out the `user: root` line from `imgur-display-setup.yml` and uncomment
  the two lines below `Vagrant setup`
* Run `vagrant up` in a terminal from within this folder
* When the Ansible provisioning completes, visit [http://localhost:8080/](localhost:8080)
  in your host machine's browser to view the running Rack app
* Run `vagrant halt` to shutdown the VM
* Run `vagrant destroy` to delete the VM's data
