# Configure webapp environment

## Create vms
```
vagrant up
```

## Configure environment
```
ansible multi -a "hostname"
ansible multi -a "hostname" -f 1
ansible multi -a "df -h"
ansible multi -a "free -m"
ansible multi -a "date"
ansible multi -m setup

# Install, configure and check chrony
ansible multi -b -m dnf -a "name=chrony state=present"
ansible multi -b -m service -a "name=chronyd state=started enabled=yes"
ansible multi -b -a "chronyc tracking"

# Install, configure and check Django
ansible app -b -m dnf -a "name=python3-pip state=present"
ansible app -b -m pip -a "executable=pip3 name=django<4 state=present"

# Install db
ansible db -b -m dnf -a "name=mariadb-server state=present"
ansible db -b -m service -a "name=mariadb state=started \
enabled=yes"

# Setup firewall
ansible db -b -m dnf -a "name=firewalld state=present"
ansible db -b -m service -a "name=firewalld state=started enabled=yes"
ansible db -b -m firewalld -a "zone=database state=present permanent=yes"
ansible db -b -m firewalld -a "source=192.168.56.0/24 zone=database state=enabled permanent=yes"
ansible db -b -m firewalld -a "port=3306/tcp zone=database  state=enabled permanent=yes"

# Configure db
ansible db -b -m dnf -a "name=python3-PyMySQL state=present"
ansible db -b -m mysql_user -a "name=django host=% password=12345 \
priv=*.*:ALL state=present"

# Run ansible playbook
ansible-playbook playbook.yml --syntax-check	# check syntax
ansible-playbook playbook.yml --list-hosts		# list of hosts that affect playbook
ansible-playbook playbook.yml									# run playbook

# Show last few lines of the messages
ansible multi -b -a "tail /var/log/messages"

# Vagrant ssh
vagrant ssh <server> # (password vagrant)
```

## Destroy vms
```
vagrant destroy
```

# Notes
- If you get an error like The authenticity of host '192.168.56.5' can't be established., this is because SSH has a security feature which requires you to confirm the server’s ‘host key’ the first time you connect. You can type yes on the command line (in this case multiple times) to dismiss the warning and accept the hostkey, or you can also set the environment variable ANSIBLE_HOST_KEY_CHECKING=False. The behavior for host key acceptance can also be configured in your SSH configuration file.


- if your user account requires a password for privilege escalation, you should also pass in -K (alias for --ask-become-pass), so you can enter your password when Ansible needs it.
