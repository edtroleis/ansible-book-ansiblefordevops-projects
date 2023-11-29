
## Error UNREACHABLE! => Failed to connect to the host via ssh

### Error details
```
TASK [Gathering Facts] *********************************************************
fatal: [drupal]: UNREACHABLE! => {"changed": false, "msg": "Failed to connect to the host via ssh: Warning: Permanently added '[172.30.96.1]:2222' (ED25519) to the list of known hosts.\r\n@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@\r\n@         WARNING: UNPROTECTED PRIVATE KEY FILE!          @\r\n@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@\r\nPermissions 0777 for '/mnt/c/Users/edtro/.vagrant.d/insecure_private_keys/vagrant.key.rsa' are too open.\r\nIt is required that your private key files are NOT accessible by others.\r\nThis private key will be ignored.\r\nLoad key \"/mnt/c/Users/edtro/.vagrant.d/insecure_private_keys/vagrant.key.rsa\": bad permissions\r\nvagrant@172.30.96.1: Permission denied (publickey,password).", "unreachable": true}

PLAY RECAP *********************************************************************
drupal                     : ok=0    changed=0    unreachable=1    failed=0    skipped=0    rescued=0    ignored=0   

Ansible failed to complete successfully. Any error output should be
visible above. Please fix these errors and try again.
```

### How to solve
- Add config.ssh properties as below in Vagrant file
```
Vagrant.configure(VAGRANTFILE_API_VERSION) do |config|
	...
	config.ssh.insert_key = false
	config.ssh.private_key_path = "~/.vagrant.d/insecure_private_key"
...
end
```

## Error he host path of the shared folder is not supported from WSL

### Error details
```
The host path of the shared folder is not supported from WSL. Host
path of the shared folder must be located on a file system with
DrvFs type. Host path: ."
```

### How to solve
- Uncomment the line 'config.vm.synced_folder ".", "/vagrant", disabled: true' in file Vagrantfile
- https://cursos.alura.com.br/forum/topico-nao-estou-conseguindo-subir-o-arquivo-vagrant-up-207665


## Error Failed to connect to the host via ssh

### Error details
```
TASK [Gathering Facts] ******************************************************************************************************************************
fatal: [192.168.56.8]: UNREACHABLE! => {"changed": false, "msg": "Failed to connect to the host via ssh: @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@\r\n@    WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!     @\r\n@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@\r\nIT IS POSSIBLE THAT SOMEONE IS DOING SOMETHING NASTY!\r\nSomeone could be eavesdropping on you right now (man-in-the-middle attack)!\r\nIt is also possible that a host key has just been changed.\r\nThe fingerprint for the ED25519 key sent by the remote host is\nSHA256:Eowbx+zsQ0gQ3a6diFsEZrtYbmG2RuB9E4+VuRqjI/0.\r\nPlease contact your system administrator.\r\nAdd correct host key in /home/edtroleis/.ssh/known_hosts to get rid of this message.\r\nOffending ECDSA key in /home/edtroleis/.ssh/known_hosts:11\r\n  remove with:\r\n  ssh-keygen -f \"/home/edtroleis/.ssh/known_hosts\" -R \"192.168.56.8\"\r\nHost key for 192.168.56.8 has changed and you have requested strict checking.\r\nHost key verification failed.", "unreachable": true}
```

### How to solve
- Add this in inventory file:
```
ansible_ssh_common_args="-o StrictHostKeyChecking=no -o UserKnownHostsFile=/dev/null"
```
