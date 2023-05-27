# Ansible Dynamic Assignments (Include) and Community Roles

[] In 

[] Create a new Branch dynamic-assignments

![dynamic-assignments branch](./Images/dynamic.png)

[] create a folder with dynamic-assignments
`mkdir dynamic-assignments`

`cd dynamic-assignments` 

[]CLone 
`git clone git@github.com:J-Raji/Project-12.git` 

[]create file env-vars.yml 

`sudo vi env-vars.yml` 

[]with

``
---
- name: collate variables from env specific file, if it exists
  hosts: all
  tasks:
    - name: looping through list of available files
      include_vars: "{{ item }}"
      with_first_found:
        - files:
            - dev.yml
            - stage.yml
            - prod.yml
            - uat.yml
          paths:
            - "{{ playbook_dir }}/../env-vars"
      tags:
        - always

``

`cd ..`

[] Create env-vars directory and 
`mkdir env-vars` 

`cd env-vars` 

[]create dev.yml,prod.yml,stage.yml and uat.yml

`sudo vi dev.yml`

`sudo vi stage.yml` 

`sudo vi uat.yml`

`sudo vi prof.yml`

[] check directory

`tree` 

![Tree list](./Images/tree.png)

## Update site.yml with dynamic assignments

[]Update site.yml with

``
---
- hosts: all
- name: Include dynamic variables 
  tasks:
  import_playbook: ../static-assignments/common.yml 
  include: ../dynamic-assignments/env-vars.yml
  tags:
    - always

-  hosts: web1-uat, web2 uat
- name: Webserver assignment
  import_playbook: ../static-assignments/webservers.yml

  ``
## Community Roles

[]Install MYSQL

`sudo apt install mysql-server`

[]Open mysql

`sudo mysql` 

[]Create MYSQL Database with roles

`ALTER USER 'root'@'172.31.3.169' IDENTIFIED WITH mysql_native_password BY 'PassWord.1';` 

## Download ansible role

`ansible-galaxy install geerlingguy.ansible `

[]confirm version of git

`git --version`

`sudo apt update` 





