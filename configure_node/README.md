configure_node
=========

This role configure and prepare a Raspberry Pi to receive a container runtime and k8s. 

Requirements
------------

Tested with Ubuntu 21.04 on Raspberry Pi 4 Model B (Python 3.9.5).

Role Variables
--------------

None, just remember check your inventory hosts.

Dependencies
------------

This role prepare the host system to receive the container runtime and k8s, has no dependencies. 

How to use: 
----------------

For use this role, create a `main.yml`:

```yaml
- hosts: all
  become: yes
  user: ubuntu      
  roles:
  - { role: configure_node, tags: ["node"] }
```

- hosts to run in all inventory hosts
- `become` is needed to run playbook with sudo privileges; 
- user by default need be `ubuntu`, or check your distro.
- set a tag for quick run after

Create your inventory file:

```
[servers]
10.100.1.11
10.100.1.12
```
To execute, call the ansible-playbook command: 

```shell
ansible-playbook -i hosts main.yml
```

License
-------

MIT

Author Information
------------------

Created by Lucas Lehnen - https://www.twitch.tv/lucas_lehnen


