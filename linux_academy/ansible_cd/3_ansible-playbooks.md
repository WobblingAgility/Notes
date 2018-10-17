Ansible Playbooks
=================

Configurint an "Ansible" Account
---------------------------------

1. Create an account for ansible to use and copy relevant ssh keys.

2. Edit the sudo file to allow the account sudo without a password. The line should look like:

`user    ALL=(ALL)       NOPASSWD: ALL`

3. Specify in `ansible.cfg` to not ask for password (comment out option).

Ansible Command Line
---------------------

View all found hosts in inventory:  
`ansible all --list-hosts`

Ansible allows specifying group. To view list of all apache web servers:  
`ansible apacheweb --list-hosts`

Ping hosts to view they are up:  
`ansible all -m ping`

To run remote commands you can use:  
`ansible apacheweb -s -m shell -a 'yum list installed | grep python'`  
_Note that -s is not needed if you configured become in ansibel.cfg_

Flags:

```
-s  is for sudo  
-m  run command module on machine  
-a  module arguments (for command what command to run)  
```

System Facts
--------------

