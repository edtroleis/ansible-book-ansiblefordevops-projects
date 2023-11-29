# Vagrant Linux - Vagrant Linux used by book

[Vagrant Boxes](https://app.vagrantup.com/boxes/search)
[geerlingguy/rockylinux8](https://app.vagrantup.com/geerlingguy/boxes/rockylinux8)

```bash
mkdir vagrant_linux
cd vagrant_linux

# vagrant box list 												# List boxes
vagrant box add geerlingguy/rockylinux8		# Add Linux box
vagrant init geerlingguy/rockylinux8			# Create a default virtual server configuration using the box

# Uncomment the line 'config.vm.synced_folder ".", "/vagrant", disabled: true' in file Vagrantfile

vagrant up																# Boot virtual server
vagrant ssh																# Login to VM

vagrant halt															# Shutdown VM
vagrant destroy														# Remove VM
```
