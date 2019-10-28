openvas
=========

<img src="https://docs.ansible.com/ansible-tower/3.2.4/html_ja/installandreference/_static/images/logo_invert.png" width="10%" height="10%" alt="Ansible logo" align="right"/>
<a href="https://travis-ci.org/robertdebock/ansible-role-openvas"><img src="https://travis-ci.org/robertdebock/ansible-role-openvas.svg?branch=master" alt="Build status" align="left"/></a>

Install and configure openvas on your system.

<img src="https://img.shields.io/ansible/role/d/30167"/>
<img src="https://img.shields.io/ansible/quality/30167"/>

Example Playbook
----------------

This example is taken from `molecule/resources/playbook.yml`:
```yaml
---
- name: Converge
  hosts: all
  become: yes
  gather_facts: yes

  roles:
    - robertdebock.openvas
```

The machine you are running this on, may need to be prepared.
```yaml
---
- name: Prepare
  hosts: all
  gather_facts: no
  become: yes

  vars:
    # ca_privatekey_path: "/var/lib/openvas/CA/cacert.pem"
    ca_requests:
      - name: clientkey
        passphrase: WoNtT3L1
        cipher: aes256
        country_name: NL
        email_address: robert@meinit.nl
        organization_name: Some Corporation
        organizational_unit_name: Department X
      - name: serverkey
        passphrase: WoNtT3L1
        cipher: aes256
        country_name: NL
        email_address: robert@meinit.nl
        organization_name: Some Corporation
        organizational_unit_name: Department X

  roles:
    - robertdebock.bootstrap
    - robertdebock.buildtools
    - robertdebock.epel
    - robertdebock.python_pip
    - robertdebock.apt_autostart
    - robertdebock.redis
    - robertdebock.ca
```

Also see a [full explanation and example](https://robertdebock.nl/how-to-use-these-roles.html) on how to use these roles.

Role Variables
--------------

These variables are set in `defaults/main.yml`:
```yaml
---
# defaults file for openvas

# The username for the openvas webinterface.
openvas_administrator_username: admin

# The password for the openvas webinterface.
openvas_administrator_password: password
```

Requirements
------------

- Access to a repository containing packages, likely on the internet.
- A recent version of Ansible. (Tests run on the current, previous and next release of Ansible.)

The following roles can be installed to ensure all requirements are met, using `ansible-galaxy install -r requirements.yml`:

```yaml
---
- robertdebock.bootstrap
- robertdebock.buildtools
- robertdebock.ca
- robertdebock.epel
- robertdebock.python_pip
- robertdebock.apt_autostart
- robertdebock.redis
- robertdebock.selinux
- robertdebock.reboot

```

This role uses the following modules:
```yaml
---
- apt_repository
- async_status
- expect
- include_role
- meta
- package
- pip
- rpm_key
- service
```

Context
-------

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://robertdebock.nl/) for further information.

Here is an overview of related roles:
![dependencies](https://raw.githubusercontent.com/robertdebock/drawings/artifacts/openvas.png "Dependency")


Compatibility
-------------

This role has been tested on these [container images](https://hub.docker.com/):

|container|tag|allow_failures|
|---------|---|--------------|
|alpine|latest|no|
|alpine|edge|yes|
|debian|stable|yes|
|debian|unstable|yes|
|debian|latest|no|
|centos|7|no|
|centos|latest|no|
|fedora|latest|no|
|fedora|rawhide|yes|
|opensuse|latest|no|
|ubuntu|rolling|yes|
|ubuntu|devel|yes|
|ubuntu|latest|no|

This role has been tested on these Ansible versions:

- ansible~=2.7
- ansible~=2.8
- git+https://github.com/ansible/ansible.git@devel

The indicator '\~=' means [compatible with](https://www.python.org/dev/peps/pep-0440/#compatible-release). For example 'ansible\~=2.8' would pick the latest ansible-2.8, for example ansible-2.8.6.

Exceptions
----------

Some variarations of the build matrix do not work. These are the variations and reasons why the build won't work:

| variation                 | reason                 |
|---------------------------|------------------------|
| CentOS 8 | Packages openvas-cli and openvas-scanner are not available. |
| ArchLinux & Ansible 2.7 | New-style module did not handle its own exit |
| OpenSUSE Leap | atomic-release Signature verification failed |

Included version(s)
-------------------

This role [refers to a version](https://github.com/robertdebock/ansible-role-openvas/blob/master/vars/main.yml) released by Atomicorp. Check the released version(s) here:
- [openvas](https://updates.atomicorp.com/channels/atomic/centos/7/x86_64/RPMS/).

This version reference means a role may get outdated. Monthly tests occur to see if [bit-rot](https://en.wikipedia.org/wiki/Software_rot) occured. If you however find a problem, please create an issue, I'll get on it as soon as possible.

Testing
-------

[Unit tests](https://travis-ci.org/robertdebock/ansible-role-openvas) are done on every commit and periodically.

If you find issues, please register them in [GitHub](https://github.com/robertdebock/ansible-role-openvas/issues)

To test this role locally please use [Molecule](https://github.com/ansible/molecule):
```
pip install molecule
molecule test
```

To test on Amazon EC2, configure [~/.aws/credentials](https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/credentials.html) and set a region using `export AWS_REGION=eu-central-1` before running `molecule test --scenario-name ec2`.

There are many specific scenarios available, please have a look in the `molecule/` directory.

License
-------

Apache-2.0


Author Information
------------------

[Robert de Bock](https://robertdebock.nl/)
