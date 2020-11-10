# ansible task
See task.txt for description of what to do. 

Ansible for solving the tasks.
Docker stuffs to try to test the ansible stuff locally.

# Task Notes

## task 1
`ansible-playbook -i DEV sudo.yml`

* install sudo 
* create group "sudo_root" gid 500
* create 3 inventory files: DEV TEST PROD
* `ansible-playbook -i DEV sudo.yml` executable command
* allow sudo access without pw for DEV+TEST
** `%sudo_root ALL=(ALL) NOPASSWD: ALL` added to /etc/sudoers
* allow sudo access WITH pw for prod
** PROD enforce pw: `%sudo_root ALL=(ALL) ALL`
* use only one task using the dev/test/prod vars. 

## task 2
Assumed that "-1.2.3" in the agent filename is referring to the actual version of the agent. 

`ansible-playbook -i FRK liagent.yml`

Link in task description is broken. Maybe it's about time to update the task?

liagent doc: https://docs.vmware.com/en/vRealize-Log-Insight/8.2/com.vmware.log-insight.agent.admin.doc/GUID-04892000-72C6-4227-BB37-6A2271E03B8C.html?hWord=N4IghgNiBcIOoHsBOBrAlgOwOYAIDuaALgBY4BuASgKaRoBeVOAMgrgJIYDOaWxhOAQSxUMhTiAC+QA

In newer version of liagent the loginsights server has taken over some of the configuration tasks such as auto_update.

liagent default config does not have auto_update of package_type, ref: https://docs.vmware.com/en/vRealize-Log-Insight/8.2/com.vmware.log-insight.agent.admin.doc/GUID-B4FCAB3D-5876-411A-885C-303EA4EF6605.html
This is now handled from the server, not the agent.


## Docker stuff for testing
Not working properly atm - ssh keys for debian containers or something makes ansible not able to log into the ssh server running in the container.
ssh with a test user works. 

### Prerequisites: 
Install: ansible, docker, docker-compose, sshpass

### Setup 
```
docker build -f debian-ssh -t debian-ssh:latest . \
  --build-arg ssh_prv_key="$(cat ~/.ssh/id_rsa)" \
  --build-arg ssh_pub_key="$(cat ~/.ssh/id_rsa.pub)"
```

`docker-compose up -d `

After starting the container we have to start the ssh service with
`service ssh start`

Then we can do 
`ssh test@172.22.11.2` pw being 'test123' as defined in the debian-ssh docker file. 


### Testing
Enter the first container to check that changes has been applied.
`docker exec -it ansible-test_dev_1 bash`



