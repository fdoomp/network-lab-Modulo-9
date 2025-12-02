# network-lab-Modulo-9

Laboratorios del modulo IX Practica 1


sudo apt update && sudo apt upgrade

sudo apt install -y libauthen-pam-perl libio-pty-perl

sudo apt --fix-broken install -y

sudo dpkg -i webmin.deb

sudo systemctl status webmin

ip add

------------------------------------------------------------------------------------------------------------

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


