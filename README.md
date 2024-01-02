# Ansible role [security](https://galaxy.ansible.com/ui/standalone/roles/buluma/security/documentation)

Security software installation and configuration.

|GitHub|Version|Issues|Pull Requests|Downloads|
|------|-------|------|-------------|---------|
|[![github](https://github.com/buluma/ansible-role-security/actions/workflows/molecule.yml/badge.svg)](https://github.com/buluma/ansible-role-security/actions/workflows/molecule.yml)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-security.svg)](https://github.com/buluma/ansible-role-security/releases/)|[![Issues](https://img.shields.io/github/issues/buluma/ansible-role-security.svg)](https://github.com/buluma/ansible-role-security/issues/)|[![PullRequests](https://img.shields.io/github/issues-pr-closed-raw/buluma/ansible-role-security.svg)](https://github.com/buluma/ansible-role-security/pulls/)|[![Ansible Role](https://img.shields.io/ansible/role/d/buluma/security)](https://galaxy.ansible.com/ui/standalone/roles/buluma/security/documentation)|

## [Example Playbook](#example-playbook)

This example is taken from [`molecule/default/converge.yml`](https://github.com/buluma/ansible-role-security/blob/master/molecule/default/converge.yml) and is tested on each push, pull request and release.

```yaml
---
- name: Converge
  hosts: all
  become: yes
  gather_facts: no

  roles:
    - role: buluma.security
      security_autoupdate_enabled: false
      security_fail2ban_enabled: false
```

The machine needs to be prepared. In CI this is done using [`molecule/default/prepare.yml`](https://github.com/buluma/ansible-role-security/blob/master/molecule/default/prepare.yml):

```yaml
---
- name: Prepare
  hosts: all
  become: yes
  gather_facts: no

  roles:
    - role: buluma.bootstrap
    - role: buluma.epel
    - role: buluma.repo_epel
      when:
        - (ansible_distribution == "Amazon" and
          ansible_distribution_major_version == "2") or
          (ansible_os_family == "RedHat" and
          ansible_distribution_major_version in [ "7", "8" ])
```

Also see a [full explanation and example](https://buluma.github.io/how-to-use-these-roles.html) on how to use these roles.

## [Role Variables](#role-variables)

The default values for the variables are set in [`defaults/main.yml`](https://github.com/buluma/ansible-role-security/blob/master/defaults/main.yml):

```yaml
---
security_ssh_port: 22
security_ssh_password_authentication: "no"
security_ssh_permit_root_login: "no"
security_ssh_usedns: "no"
security_ssh_permit_empty_password: "no"
security_ssh_challenge_response_auth: "no"
security_ssh_gss_api_authentication: "no"
security_ssh_x11_forwarding: "no"
security_sshd_state: started
security_ssh_restart_handler_state: restarted
security_ssh_allowed_users: []
security_ssh_allowed_groups: []

security_sudoers_passwordless: []
security_sudoers_passworded: []

security_autoupdate_enabled: false
security_autoupdate_blacklist: []
security_autoupdate_secpkgs_only: false

# Autoupdate mail settings used on Debian/Ubuntu only.
security_autoupdate_reboot: "false"
security_autoupdate_reboot_time: "03:00"
security_autoupdate_mail_to: ""
security_autoupdate_mail_on_error: true

security_fail2ban_enabled: true
security_fail2ban_custom_configuration_template: "jail.local.j2"
```

## [Requirements](#requirements)

- pip packages listed in [requirements.txt](https://github.com/buluma/ansible-role-security/blob/master/requirements.txt).

## [State of used roles](#state-of-used-roles)

The following roles are used to prepare a system. You can prepare your system in another way.

| Requirement | GitHub | Version |
|-------------|--------|--------|
|[buluma.bootstrap](https://galaxy.ansible.com/buluma/bootstrap)|[![Ansible Molecule](https://github.com/buluma/ansible-role-bootstrap/actions/workflows/molecule.yml/badge.svg)](https://github.com/buluma/ansible-role-bootstrap/actions/workflows/molecule.yml)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-bootstrap.svg)](https://github.com/shadowwalker/ansible-role-bootstrap)|
|[buluma.epel](https://galaxy.ansible.com/buluma/epel)|[![Ansible Molecule](https://github.com/buluma/ansible-role-epel/actions/workflows/molecule.yml/badge.svg)](https://github.com/buluma/ansible-role-epel/actions/workflows/molecule.yml)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-epel.svg)](https://github.com/shadowwalker/ansible-role-epel)|
|[buluma.repo_epel](https://galaxy.ansible.com/buluma/repo_epel)|[![Ansible Molecule](https://github.com/buluma/ansible-role-repo_epel/actions/workflows/molecule.yml/badge.svg)](https://github.com/buluma/ansible-role-repo_epel/actions/workflows/molecule.yml)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-repo_epel.svg)](https://github.com/shadowwalker/ansible-role-repo_epel)|

## [Context](#context)

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://buluma.github.io/) for further information.

Here is an overview of related roles:

![dependencies](https://raw.githubusercontent.com/buluma/ansible-role-security/png/requirements.png "Dependencies")

## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/buluma):

|container|tags|
|---------|----|
|[EL](https://hub.docker.com/repository/docker/buluma/enterpriselinux/general)|all|
|[Fedora](https://hub.docker.com/repository/docker/buluma/fedora/general)|all|
|[Debian](https://hub.docker.com/repository/docker/buluma/debian/general)|all|
|[Ubuntu](https://hub.docker.com/repository/docker/buluma/ubuntu/general)|all|
|[Kali](https://hub.docker.com/repository/docker/buluma/kali/general)|all|

The minimum version of Ansible required is 2.12, tests have been done to:

- The previous version.
- The current version.
- The development version.

If you find issues, please register them in [GitHub](https://github.com/buluma/ansible-role-security/issues)

## [Changelog](#changelog)

[Role History](https://github.com/buluma/ansible-role-security/blob/master/CHANGELOG.md)

## [License](#license)

[Apache-2.0](https://github.com/buluma/ansible-role-security/blob/master/LICENSE)

## [Author Information](#author-information)

[Shadow Walker](https://buluma.github.io/)

