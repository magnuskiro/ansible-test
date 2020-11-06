# ansible task
Interview task for devops analyst. 
creating an ansible setup with 6 nodes, 2 inventories, 3 environments

## Tested environment
linux mint (ubuntu sort)

## Prerequisites: 
Install: ansible, docker, docker-compose

## Setup 
`docker build -f debian-ssh -t debian-ssh:latest .`

`docker-compose up -d `

After starting the container we have to start the ssh service with
`service ssh start`

Then we can do 
`ssh test@172.22.11.2` pw being 'test123' as defined in the debian-ssh docker file. 


## Testing
Enter the first container to check that changes has been applied.
`docker exec -it vipps-test_dev_1 bash`

## Run ansible
... test commands go here.


# TODOS

## 1

* install sudo 
* create group "sudo_root" gid 500
* create 3 inventory files: DEV TEST PROD
* `ansible-playbook -i DEV sudo.yml` executable command
* allow sudo access without pw for DEV+TEST
** `%sudo_root ALL=(ALL) NOPASSWD: ALL` added to /etc/sudoers
* allow sudo access WITH pw for prod
** PROD enforce pw: `%sudo_root ALL=(ALL) ALL`
* use only one task using the dev/test/prod vars. 

## 2
...
fetch LogInsights agent for installation on nodes. 

* Dockerfile with commands for running ansible stuff on all the containers.