Setup and Configuration
=======================

Configuration
-------------

3 servers

Server:  
dbuckley1.mylabserver.com (control)  
dbuckley2.mylabserver.com (web)   
dbuckley3.mylabserver.com (app)

Playbooks are run from the workstation

Download and Installation
-------------------------

There is a paid version know as ansible tower which includes support. This is adventageous for companies where ansible is an essential tool.

the free ansible is available in all linux distro repositories.

It can be installed on rpm based with `yum isntall ansible`. CentOS may need the `epel-repo` installed first.

Ansible Configuration File
--------------------------

The configuration file is `/etc/ansible/ansible.cfg`

Default setup is under `/etc/ansible` and includes ansible.cfg, hosts, and a roles directory. This is the typical structure.

Can be in the current dir, `~/.ansible`, or in `/etc/ansible`. All options can be overwritten in the command called or the playbook.

Note worthy options inside the ansible config file:  
- `inventory` where to find the hosts file with list of hosts.
- `pattern`, `forks`, and `poll_interval` are for performance and parallel tasks.
- `sudo_user` who to become for administration (should always be root and is depreciated).
- `become_user` is the new way to specify who to use to administrate. Replaces `sudo_user`
- `ask_sudo_pass` or `ask_pass` for whether to ask for a password when using sudo. Alternatively can be a key exchange.
- `roles_path` where to find roles used.
- `remote_user` for who to connect as.
- `log_path` should be enabled when creating playbooks for troubleshooting. It can grow fast so if using for production, rotate the log.

There is plenty of tweeking for warning of issues in the config file.

The HOSTS File
---------------

Inventory is grouped like so:

```
[group]  
host1  
host2  
```

Overriding the Default HOSTS File
---------------------------------

To override the `ansible.cfg` hosts file you can run ansible with a `-i` flag and the path to the hosts file to use.

Overriding the Default System `ansible.cfg` File
--------------------------------------------------

You can also create a `ansible.cfg` in the current dir to set your own hosts file.

A third option would be to use a custom `ansible.cfg` at `~.ansible.cfg`.

Overriding the Default Roles Path
---------------------------------

As stated above you can add locations where to search for roles in the `ansible.cfg` file. You can use this to add roles from other locations and to use third party roles.

Ansible searches for roles in the order specified in the `ansible.cfg` to avoid name collisions.