![alt text](swclogo.jpg)
# swc_rsnapshot
* This repository contains playbooks to install rsnapshot on RHEL8 and back a known good configuration of /etc using rsnapshot, it also will restore files changed post alpha0 and restore any modified files and save off the files that were changed. For any additional details or inquiries, please contact us at christopher.sargent@railhead.io.

* [Rsnapshot](https://github.com/rsnapshot/rsnapshot)

# swc_rsnapshot_installer 
* Run swc_rsnapshot_installer role to create a backup of known good /etc. Note that is stored at /.snapshots/alpha.0/localhost/etc/
1. git clone
2. cd 
3. vim swc_rsnapshot.yml
```
---
  - name: swc_rsnapshot_restore
    hosts: all
    gather_facts: yes
    become_user: root
    tasks:
    - name: swc_rsnapshot_install
      include_role:
        name: swc_rsnapshot_install

#   - name: swc_rsnapshot_restore
#      include_role:
#        name: swc_rsnapshot_restore
```
4. Configure AAP/AWX for inventory, credentials, project and template
5. Launch swc_rsnapshot to install epel and rsnapshot and create a backup of known good /etc located at /.snapshots/alpha.0/localhost/etc/

![Screenshot](resources/screenshot01.png)

6. modify /etc/ssh/sshd_config and /etc/hosts
* for testing purposes

7. vim swc_rsnapshot.yml
```
---
  - name: swc_rsnapshot_restore
    hosts: all
    gather_facts: yes
    become_user: root
    tasks:
#    - name: swc_rsnapshot_install
#      include_role:
#        name: swc_rsnapshot_install

   - name: swc_rsnapshot_restore
      include_role:
        name: swc_rsnapshot_restore
```
8. Launch swc_rsnapshot to locate changed files, restore them and create a directory of the files that were modified post alpha.0
* Located at /review/changed_files

![Screenshot](resources/screenshot02.png)

![Screenshot](resources/screenshot03.png)