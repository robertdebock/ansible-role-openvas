openvas
=========

[![Build Status](https://travis-ci.org/robertdebock/ansible-role-openvas.svg?branch=master)](https://travis-ci.org/robertdebock/ansible-role-openvas)

Provides openvas for your system.


Example Playbook
----------------

This example is taken from `molecule/default/playbook.yml`:
```
---
- name: Converge
  hosts: all
  gather_facts: false
  become: true

  roles:
    - robertdebock.bootstrap
    - robertdebock.buildtools
    - robertdebock.epel
    - robertdebock.python_pip
    - robertdebock.redis
    - robertdebock.openvas

```

Role Variables
--------------

These variables are set in `defaults/main.yml`:
```
---
# defaults file for openvas

# The username for the openvas webinterface.
openvas_administrator_username: admin

# The password for the openvas webinterface.
openvas_administrator_password: password

# To update all packages installed by this roles, set `openvas_package_state` to `latest`.
openvas_package_state: present

```

Requirements
------------

- Access to a repository containing packages, likely on the internet.
- A recent version of Ansible. (Tests run on the last 3 release of Ansible.)

The following roles can be installed to ensure all requirements are met, using `ansible-galaxy install -r requirements.yml`:

---
- robertdebock.bootstrap
- robertdebock.buildtools
- robertdebock.epel
- robertdebock.python_pip
- robertdebock.redis
- robertdebock.selinux
- robertdebock.reboot


Context
-------

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://robertdebock.nl/) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/robertdebock/drawings/artifacts/openvas.png "Dependency")


Compatibility
-------------

This role has been tested against the following distributions and Ansible version:

|distribution|ansible 2.4|ansible 2.5|ansible 2.6|ansible 2.7|ansible devel|
|------------|-----------|-----------|-----------|-----------|-------------|
|alpine-edge*|yes|yes|yes|yes|yes*|
|alpine-latest|yes|yes|yes|yes|yes*|
|archlinux|yes|yes|yes|yes|yes*|
|centos-6|no|no|no|no|yes*|
|centos-latest|yes|yes|yes|yes|yes*|
|debian-latest|yes|yes|yes|yes|yes*|
|debian-stable|yes|yes|yes|yes|yes*|
|debian-unstable*|yes|yes|yes|yes|yes*|
|fedora-latest|yes|yes|yes|yes|yes*|
|fedora-rawhide*|no|no|no|no|no*|
|opensuse-leap|no|no|no|no|yes*|
|opensuse-tumbleweed|no|no|no|no|yes*|
|ubuntu-artful|no|no|no|no|yes*|
|ubuntu-devel*|yes|yes|yes|yes|yes*|
|ubuntu-latest|yes|yes|yes|yes|yes*|

A single star means the build may fail, it's marked as an experimental build.

Testing
-------

[Unit tests](https://travis-ci.org/robertdebock/ansible-role-openvas) are done on every commit and periodically.

If you find issues, please register them in [GitHub](https://github.com/robertdebock/ansible-role-openvas/issues)

To test this role locally please use [Molecule](https://github.com/metacloud/molecule):
```
pip install molecule
molecule test
```
There are many specific scenarios available, please have a look in the `molecule/` directory.


License
-------

Apache-2.0


Author Information
------------------

[Robert de Bock](https://robertdebock.nl/) <robert@meinit.nl>
