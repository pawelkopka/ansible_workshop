## Inventory
Ansible expect inventory in dir ```/etc/ansible/hosts```,but you can use flag ```-i```
### ini 
```bash
cat inventory
```
### yaml
```bash
cat inventory.yaml
```
### dynamic
some python code, with correct output(check doc)

## Modules

## ping
```bash
ansible -i inventory.yaml centos -m ping
```

```bash
ansible -i inventory.yaml group_apt -m ping
```

## setup - show variables
```bash
ansible -i inventory.yaml ubuntu -m setup
```


## *verbose 
```bash
ansible -vvv -i inventory.yaml centos -m ping
```

## shell
```bash
ansible -i inventory.yaml centos -m shell  -a "uname"
```

## yum/apt
```bash
ansible --become -i inventory.yaml centos -m yum -a "name=tcpdump state=present"
```
```bash
ansible --become -i inventory.yaml centos -m yum -a "name=tcpdump state=absent"
```

## Playbooks

