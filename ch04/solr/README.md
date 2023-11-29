# Apache Solr server
- Apache Solr
- Java
- Ubuntu LTS

# Build and destroy environment
```
vagrant up
vagrant destroy --force
```

# Run Ansible playbook
```
ansible-playbook playbook.yml --syntax-check
ansible-playbook playbook.yml --list-hosts
ansible-playbook playbook.yml
```

## Access server page
http://192.168.56.9:8983/solr
