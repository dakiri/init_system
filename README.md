The aim is to prepare the system for automation by creating an account dedicated to ansible jobs.
Depending of the accounts created on the system.

Initial system :

*  root account can log with a ssh key

inventory:
```
     host1:
         ansible_ssh_private_key_file: "~/.ssh/id_initialLogin"
         ansible_user: "root"
```

```
ansible-playbook init_system/playbook.yml -i inventory_redteams.yml
```


* privilege account can sudo

inventory
```
     host1:
         ansible_user: "admin"
         become_method: "sudo"
```

```
ansible-playbook init_system/playbook.yml -i inventory_redteams.yml  -K --ask-pass
```

* unprivilege account and need to su

inventory
```
     host1:
         ansible_user: "admin"
         become_method: "su"
```

```
ansible-playbook init_system/playbook.yml -i inventory_redteams.yml  -K --ask-pass
```

# Inventory example

```
myhosts:

  hosts:
     host1:
         ansible_ssh_private_key_file: "~/.ssh/id_initialLogin"
         ansible_user: "root"

     host2:
         ansible_user: "admin"
         become_method: "su"

  vars:

     system:
        ansible_user: "user-ansible"
        ansible_pub_key: "~/.ssh/id_ecdsa.pub"
```


