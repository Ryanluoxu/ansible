# ansible

source:[ansible tutorial](https://serversforhackers.com/c/an-ansible-tutorial)

## inventory file
/etc/ansible/hosts

## adhoc command
ansible all -m ping

## modules
ansible all -m shell -a 'apt-get install nginx'

## playbook
ansible-playbook  nginx.yml

### handlers
```
---
- hosts: local
  tasks:
   - name: Install Nginx
     apt: pkg=nginx state=installed update_cache=true
     notify:
      - Start Nginx

  handlers:
   - name: Start Nginx
     service: name=nginx state=started
```

## role
server.yml
```
---
- hosts: all
  roles:
    - nginx
```

`ansible-playbook server.yml`

rolename
 - files : no main.yml
 - handlers
 - meta
 - templates : no main.yml instead serversforhackers.com.conf
 - tasks
 - vars

## facts
system information: ansible_processor_cores, ansible_distribution_release

## vault
```bash
ansible-vault create vars/main.yml
ansible-vault edit vars/main.yml
mkpasswd --method=SHA-512 # create password hash
ansible-playbook --ask-vault-pass provision.yml
```
