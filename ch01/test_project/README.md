# Run Ansible - simple example

## Install packages
```
sudo apt install
sudo apt install -y \
	vim \
	python3-pip \
	openssh-client

pip3 install ansible
```

## Set vim profile
```
cat > .vimrc << EOF
:set number
:set cursorcolumn
EOF
```

## Create Ansible project
```
mkdir test_project
cd test_project
```

## Create inventory
```
cat > hosts.ini << EOF
[example]
localhost
EOF
```

## Test inventory
```
ansible -i hosts.ini all -m ping --connection=local
```

## Show memory statistic (free -h)
```
ansible -i hosts.ini example -a "free -h" --connection=local
```
