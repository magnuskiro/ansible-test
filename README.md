# ansible task
Interview task for devops analyst. 
creating an ansible setup with 6 nodes, 2 inventories, 3 environments

## Prerequisites: 
Install: ansible, docker, docker-compose

## Setup 
`docker-compose up -d `

## Testing
Enter the first container to check that changes has been applied.
`docker exec -it vipps-test_dev_1 bash`

## Run ansible
...


# TODOS

## 1

* install sudo 
* create group "sudo_root" gid 500
* create 3 inventory files: DEV TEST PROD
* `ansible-playbook -i DEV sudo.yml` executable command
* allow sudo access without pw for DEV+TEST
** `%sudo_root ALL=(ALL) NOPASSWD: ALL` added to /etc/sudoers
** PROD enforce pw: `%sudo_root ALL=(ALL) ALL`
* use only one task using the dev/test/prod vars. 

## 2
...