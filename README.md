# Vagrant Jenkins Installation 

## Prerequisites
### Ansible Installation:
Ansible by default manages machines over the SSH protocol.
For installation and additional information please visit: 
https://docs.ansible.com/ansible/latest/installation_guide/intro_installation.html

### Virtual Box Download:
VirtualBox is a general-purpose full virtualizer for x86 hardware, targeted at server, desktop and embedded use. 
To download Virtual Box head to https://www.virtualbox.org/wiki/Downloads
### Vagrant Installation 
Head over to the https://www.vagrantup.com/downloads.html and get the appropriate installer or package for your platform. Install the package using standard procedures for your operating system. For additional Information head over to: https://www.vagrantup.com/docs/installation/

### Also knowledge of python is required

## Running

#### Ansible
Ansible is an extra-simple tool/framework/API for doing ‘remote things’. this command allows you to define and run a single task ‘playbook’ against a set of hosts
To begin, run the Ansible command: 
ansible-playbook site.yml-f 10

To checkout a repo of configuration instructions from git use the command The ansible-pull  and then run ansible-playbook against the content. 
For additional information on Ansible Pull run the ansible-pull –help command.
#### Vagrant
The Vagrant Ansible provisioner allows you to provision the guest using Ansible playbooks by executing ansible-playbook from the Vagrant host.
After installation, Jenkins will be available at http://local-ip:8080, with a default user/pass of admin/admin.
To start create a Vagrantfile and customize as the user desires 
Below there are standard commands that are required when using a provisioner for Vagrant: 
vagrant up - creates a new vagrant box and runs through the provisioning steps in the Vagrant file
vagrant provision - runs the provisioning steps against an existing Vagrant VM
vagrant suspend - shuts down the vm and saves state
vagrant resume - resumes running a previously saved VM
vagrant destroy - shuts down and removes a Vagrant VM
You can add the --provision flag to any vagrant up/resume to force a reprovisioning of the machine.

## Configuration
To local IP is setup: 
Change the local IP of the Jenkins installation by editing `vagrant-config.yml`
1. Set the `local_ip` value for the reserved IP range you want to use.
2. Set the `usethis` value to the configuration block you want to use (`one_nine_two`|`ten`|`one_seven_two`)
To run Ansible against your Vagrant guest, the basic Vagrantfile configuration looks like:

```c
Vagrant.configure("2") do |config|

  #
  # Run Ansible from the Vagrant Host
  #
  config.vm.provision "ansible" do |ansible|
    ansible.playbook = "playbook.yml"
  end

end
```


