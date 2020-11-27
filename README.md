Ansible role: Terraform
=========

This role helps you to install mysql on your linux machine.


|Travis|GitHubActions|Quality|Downloads|Version|
|------|-------------|-------|---------|-------|
|[![travis](https://travis-ci.com/amine7777/ansible-role-mysql.svg?branch=master)](https://travis-ci.com/amine7777/ansible-role-mysql)|[![github](https://github.com/amine7777/ansible-role-mysql/workflows/CI/badge.svg)](https://github.com/amine7777/ansible-role-mysql/actions)|[![quality](https://img.shields.io/ansible/quality/52042)](https://galaxy.ansible.com/amine7777/mysql)|[![downloads](https://img.shields.io/ansible/role/d/52042)](https://galaxy.ansible.com/amine7777/mysql)|[![Version](https://img.shields.io/github/release/amine7777/ansible-role-mysql.svg)](https://github.com/amine7777/ansible-role-mysql/releases/)|

![](mysql.jpg)

Requirements
------------
- Linux machine
- Ansible 2.10

Role Variables
--------------
These variables help you to manage mysql installation.

You can specify your mysql root password in this variable.
```yaml
mysql_root_password: changemeplease
```
By setting the root password you can create users using ***mysql_users*** list.
Here you add users with privilleges to databases or tables.
```yaml
mysql_users:
  - name: john
    password: doe
    host: localhost
    priv: "mydatabase.*:ALL"
    state: present

  - name: jess
    password: doe
    host: localhost
    priv: "*.*:ALL"
    state: present
```
After settings the users you can create the databases with the appropriate users.
```yaml
mysql_databases:
  - name: mydatabase
    login_user: john
    login_password: doe
    state: present

  - name: mydatabase
    login_user: jess
    login_password: doet
    state: present
```

Example Playbook
----------------

```yaml
- hosts: all
  vars:
    mysql_users:
      - name: john
        password: doe
        host: localhost
        priv: "mydatabase.*:ALL"
        state: present

    mysql_databases:
      - name: mydatabase
        login_user: john
        login_password: doe
        state: present
  roles:
     - amine7777.mysql
```

Author Information
------------------

- [Amine Kahlaoui](https://github.com/amine7777), DevOps engineer.
