# Setup environment - WSL2 + VirtualBox + Vagrant
- [Vagrant on WSL2](https://blog.thenets.org/how-to-run-vagrant-on-wsl-2/)

## Install Virtualbox on Windows
```bash
choco install virtualbox
```

## Install Vagrant on WSL2 Ubuntu
- [Install Vagrant](https://developer.hashicorp.com/vagrant/install?product_intent=vagrant)
```bash
wget -O- https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg

echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list

sudo apt update && sudo apt install vagrant

vagrant --version
```

## Configure .bashrc
```bash
echo 'export VAGRANT_WSL_ENABLE_WINDOWS_ACCESS="1"' >> ~/.bashrc
echo 'export PATH="$PATH:/mnt/c/Program Files/Oracle/VirtualBox"' >> ~/.bashrc

source ~/.bashrc
```

## Install virtualbox_WSL2 plugin
```bash
vagrant plugin install virtualbox_WSL2
```

# Vagrant hello world
```bash
# Go to Windows user's dir from WSL
cd /mnt/c/Users/<my-user-name>/

# Create a project dir
mkdir -p projects/vagrant-demo
cd projects/vagrant-demo

# Create a Vagrantfile using Vagrant CLI
vagrant init hashicorp/bionic64
ls -l Vagrantfile

# Uncomment the line 'config.vm.synced_folder ".", "/vagrant", disabled: true' in file Vagrantfile

# Start a VM using Vagrantfile
vagrant up

# Login to the VM
# (password is 'vagrant')
vagrant ssh
```
