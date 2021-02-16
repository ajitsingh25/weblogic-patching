## weblogic-patching
Stage and Prod Weblogic Patching


### Always verify  Patch Variables File [group_vars/all](https://github.com/ajitsingh25/weblogic-patching/blob/master/group_vars/all)
```
view group_vars/all
```
#### Host Inventory Sample
```
[all]  
stage2cppxyz

[all:vars]  
ansible_python_interpreter=/x/opt/pp/bin/python  
ansible_ssh_extra_args='-o StrictHostKeyChecking=no'
```

#### 1. [list_patch.yml](https://github.com/ajitsingh25/weblogic-patching/blob/master/list_patch.yml)  List Patch
```
ansible-playbook -i inventory/stage/202 --ask-become-pass list_patch.yml -k
```

#### 2. [apply.yml](https://github.com/ajitsingh25/weblogic-patching/blob/master/apply.yml)  Apply Patch
```
ansible-playbook -i inventory/stage/202 --ask-become-pass apply.yml -k --skip-tags debug
```

#### 3. [rollback.yml](https://github.com/ajitsingh25/weblogic-patching/blob/master/rollback.yml) Rollback Patch
```
ansible-playbook -i inventory/stage/202 --ask-become-pass rollback.yml -k --skip-tags debug
```

#### 4. [restart_nm.yml](https://github.com/ajitsingh25/weblogic-patching/blob/master/restart_nm.yml) Restart Node Manager
```
ansible-playbook -i inventory/stage/084 --ask-become-pass restart_nm.yml -k --skip-tags debug
```

#### 5. Working on hosts with logins "su - website"  
```
ansible-playbook -i inventory/live/su-host list_patch.yml --become-method=su --ask-become-pass -k
```
