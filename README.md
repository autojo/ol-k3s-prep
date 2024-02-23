ol-k3s-prep
=========

A role to do some preparations on oracle linux 9 with selinux enabled to run k3s on top of it.

Requirements
------------

A webserver with context webserver.my.domain/k3s with the following files
* k3s-selinux policy

```bash
k3s
└── k3s-selinux-1.4-1.el9.noarch.rpm
```

Role Variables
--------------

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.


Example Playbook
----------------

```yaml
---

- name: Prepare k3s nodes
  hosts: k3s_cluster
  remote_user: root
  become: true
  vars:
    webserver: 'http://webserver.my.domain/k3s'
    k3s_allow_os_upgrade: true
    k3s_selinux_policy: k3s-selinux-1.4-1.el9.noarch.rpm
    k3s_interface_name: enp0s3
    k3s_keepalived: true
    k3s_api_ip: 192.168.1.100
    k3s_release_version: v1.27.1+k3s1

  roles:
    - ol-k3s-prep

...
```

Example Inventory
-----------------
```yaml
---
k3s_cluster:
  hosts:
    node1.my.domain:
      k3s_control_node: true
    node2.my.domain:
      k3s_control_node: true
    node3.my.domain:
      k3s_control_node: true
...
```

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
