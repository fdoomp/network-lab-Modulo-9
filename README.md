# network-lab-Modulo-9

Laboratorios del modulo IX Practica 1


sudo apt update && sudo apt upgrade

sudo apt install -y libauthen-pam-perl libio-pty-perl

sudo apt --fix-broken install -y

sudo dpkg -i webmin.deb

sudo systemctl status webmin

ip add

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Laboratorios del modulo IX Practica 2

wget -O - https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(grep -oP '(?<=UBUNTU_CODENAME=).*' /etc/os-release || lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list
sudo apt update && sudo apt install terraform

ssh-keygen -t rsa -b 4096 -C "terraform_key"

cat -/.ssh/id_rsa.pub

sudo nano terraform.tfvars

do_token    = ""
ssh_key_id  = ""


sudo nano main.tf

terraform {
  required_providers {
    digitalocean = {
      source  = "digitalocean/digitalocean"
      version = "~> 2.0"
    }
  }
}

provider "digitalocean" {
  token = var.do_token
}

resource "digitalocean_droplet" "web" {
  image    = "ubuntu-22-04-x64"
  name     = "OSvvm"
  region   = "nyc1"
  size     = "s-1vcpu-1gb"
  ssh_keys = [var.ssh_key_id]
}

variable "do_token" {
  description = "DigitalOcean Personal Access Token"
  type        = string
}

variable "ssh_key_id" {
  description = "ID de la llave SSH cargada en DigitalOcean"
  type        = string
}


sudo nano terraform.tfvars 
 

do_token    = "dop_v1_57a50f09f5152197bd2549acb4ce8b2d1331f492c4ce4bbb40bfbedfb3bcd"
ssh_key_id  = "a2:22:df:42:7c:07:e1:d3:be:fa:69:8d:bd:fa:2e:"

terraform init
terraform plan
terraform apply

terraform show | grep ipv4_address

ssh root@la-ip-publica

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Laboratorios del modulo IX Practica 3

sudo apt install ansible -y

sudo mkdir -p /etc/ansible/

sudo nano ansible.cfg

[defaults]
inventory = /etc/ansible/hosts
private_key_file = /home/ansible/.ssh/id_rsa
host_key_checking = False
ask_become_pass = True

[ssh_connection]
ssh_args = -o ForwardAgent=yes -o ControlMaster=auto -o ControlPersist=60s



sudo nano /etc/ansible/hosts

[win]
ip de maquina windows vm 

[win:vars]
ansible_user=ansible
ansible_password=1234
ansible_port=5985
ansible_connection=winrm
ansible_winrm_transport=basic
ansible_winrm_server_cert_validation=ignore

[linux]
la ip de la maquina ocean 

[linux:vars]
ansible_user=ansible
ansible_ssh_private_key_file=~/.ssh/id_rsa
ansible_become_password=1234


ssh-keygen -t rsa -b 4096

cat ~/.ssh/id_rsa.pub

adduser ansible

usermod -aG sudo ansible 

chsh -s /bin/bash ansible 

sudo mkdir -p /home/ansible/.ssh

sudo chmod 700 /home/ansible/.ssh

sudo nano /home/ansible/.ssh/authorized_keys

sudo chmod 600 /home/ansible/.ssh/authorized_keys

sudo chown -R ansible:ansible /home/ansible.ssh


ansible Linux -m ping -u ansible 


Set-ExecutionPolicy RemoteSigned -Force

Enable-PSRemoting -Force

Set-Item WSMan:\localhost\Service\AllowUnencrypted -Value $true
Set-Item WSMan:\localhost\Service\AuthiBasic -Value $true
Set-Item WSMan:\localhost\Client\TrustedHosts -Value '*' -Force

netsh advfirewall firewall add rule name="WinRM HTTP" dir=in action=allow protocol=TCP localport=5985

netsh advfirewall firewall set rule group="Administración remota de Windows" new enable=yes

Restart-Service WinRM

$Password = ConvertTo-SecureString "1234" -AsPlainText -Force

New-LocalUser -Name "ansible" -Password $Password -FullName "Ansible User" -Description "Usuario para Ansible"

Add-LocalGroupMember -Group "Administrators" -Member "ansible"

winrm enumerate winrm/config/listener

Test-NetConnection -ComputerName localhost -Port 5985

ansible win -m win_ping 


------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Laboratorios del modulo IX Practica 4

ansible win -i /etc/ansible/hosts -m win_shell -a 'echo "Archivo de prueba ad-hoc" > C:/Users/andry/Desktop/pruebadhoc.txt'


ansible win -i /etc/ansible/hosts -m win_shell -a 'Move-Item -Path "C:/Users/andry/Desktop/pruebadhoc.txt" -Destination "C:/Users/andry/Documents/"'



ansible win -i /etc/ansible/hosts -m win_shell -a 'Test-Path "C:/Users/andry/Documents/pruebadhoc.txt"'

ping 134.209.114.221

ansible 134.209.114.221 -i /etc/ansible/hosts -m reboot -become 

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Laboratorios del modulo IX Practica 5




