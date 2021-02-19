# Ansible demo: create docker containers using Ansible
### Contents
- `dockerhost` and `ansible`: two up hosts/vm's, mandatory for this demo!
- two folder with content requirements for each of above hosts,<br/>
  for vm/machine `ansible`, folder=ansible,for vm/machine `dockerhost`, folder=dockerhost

### Get started
- git clone https://github.com/mihaivirlan/create-docker-containers-using-ansible
- cd path_to_new_cloned_repository
- edit your local /etc/hosts file and add inside, the hostname and ip address for `ansible` machine
- open terminal/shell and connect on `ansible` vm/host through ssh: ssh `ansible`
- after connected, from `ansible` machine, <br/>
  edit and add your hostname and ip address for `dockerhost` machine in /etc/hosts, <br/>
  generate the ssh key, <br/>
  and transfer the ssh public key to `dockerhost` machine/vm: ssh-copy-id `dockerhost`
- after transfer successfully ssh public key,<br/> 
  try to connect from `ansible` machine to `dockerhost` machine,<br/> 
  you should connect/login successfully through ssh, if you successfully transferred the public key

### Install/setting up the ansible on your `ansible` machine:
- sudo su -
- apt update; apt install ansible
- ansible --version
- nano /etc/ansible/hosts (edit and add follow entry at the end of the file)<br/>
[servers]<br/>
dockerhost ansible_host=192.168.8.108<br/>
[all:vars]<br/>
ansible_python_interpreter=/usr/bin/python3

- ansible servers -m ping

# Pull centos image, running ansible-playbook
### From `dockerhost` machine:
- sudo su -
- install/setting up docker
- docker -v
- docker images

### From `ansible` machine:
- sudo su -
- cd test
- ansible-playbook pull_image.yml

### From `dockerhost` machine:
- sudo su -
- docker images

# Create the custom image, running ansible-playbook
### From `ansible` machine:
- sudo su -
- cd test
- ansible-playbook create_image.yml

### From `dockerhost` machine:
- sudo su -
- docker images


# Create container, running ansible-playbook
### From `ansible` machine:
- sudo su -
- cd test
- ansible-playbook create_container.yml

### From `dockerhost` machine:
- sudo su -
- docker ps -a
- Also, test the running container from your browser - `your_ip_address_dockerhost_machine:8080`

# Validation module for dockerhost
### From `ansible` machine:
- sudo su -
- cd test
- ansible-playbook dockerhost_validator.yml