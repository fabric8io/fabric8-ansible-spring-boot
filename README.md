# Kansible demo for Spring Boot

This is a simple example of provisioning an executable Spring Boot jar with Ansible.

# Environment (machines)

We use Ansible to install the Java App on application servers (```appservers``` group).

# How to use it

Required software:
>
 * *Vagrant* (https://www.vagrantup.com/) **version 1.7.0 or later<sup>1</sup>** - requires any virtualization software (e.g. VirtualBox)
 * *Ansible* (http://ansible.com/) **version 1.9 or later**

You can download latest version of Vagrant from its homepage. Ansible can be installed using system package manager or ```pip```.

Required hardware:

 * Linux like operating system
 * at least 2GB of RAM (each machine from this sample uses at most 512MB of RAM).

## Start machines

To test Ansible scripts you need to start vagrant machines. We provide ```Vagrantfile``` with suitable configuration. To start all machines invoke command:
```bash
vagrant up
```

Starting machines for the first time might take few minutes, since Vagrant has to download CentOS image.

## Provision machines

Provisioning is done by Ansible. On application servers Ansible scripts install and configure Oracle Java JRE and the App.
Invoke this command to provision all machines:
```bash
ansible-playbook -i inventory provisioning/site.yml -vv --ask-vault-pass
```

### Ansible Vault

During the provisioning you will be prompted for Ansible Vault password, type: ```vault```. It is used for decrypting ```vault.yml``` file which holds the credentials for HAProxy statistics page. You can view the statistics page by accessing following address: ```http://10.10.1.10:8080```. Default credentials are - user: ```admin``` password: ```password```.

Open your web browser, application is available at ```http://10.10.1.20/8080/```.

- - -

**1**: Since v.1.7.0  Vagrant has started generating separate SSH key for each machine making provisioning process more difficult. In prior version there was only a single key for all of the machines - ```~/.vagrant.d/insecure_private_key```. After v.1.7.0 each machine has its own key located in ```.vagrant/machines/<<machine name>>/virtualbox/private_key```. For further details see: [Using Vagrant and Ansible: Running Ansible Manually](http://docs.ansible.com/guide_vagrant.html#running-ansible-manually)
