# [security](#security)

Security software installation and configuration.

|GitHub|GitLab|Quality|Downloads|Version|Issues|Pull Requests|
|------|------|-------|---------|-------|------|-------------|
|[![github](https://github.com/buluma/ansible-role-security/workflows/Ansible%20Molecule/badge.svg)](https://github.com/buluma/ansible-role-security/actions)|[![gitlab](https://gitlab.com/buluma/ansible-role-security/badges/master/pipeline.svg)](https://gitlab.com/buluma/ansible-role-security)|[![quality](https://img.shields.io/ansible/quality/58018)](https://galaxy.ansible.com/buluma/security)|[![downloads](https://img.shields.io/ansible/role/d/58018)](https://galaxy.ansible.com/buluma/security)|[![Version](https://img.shields.io/github/release/buluma/ansible-role-security.svg)](https://github.com/buluma/ansible-role-security/releases/)|[![Issues](https://img.shields.io/github/issues/buluma/ansible-role-security.svg)](https://github.com/buluma/ansible-role-security/issues/)|[![PullRequests](https://img.shields.io/github/issues-pr-closed-raw/buluma/ansible-role-security.svg)](https://github.com/buluma/ansible-role-security/pulls/)|

## [Example Playbook](#example-playbook)

This example is taken from `molecule/default/converge.yml` and is tested on each push, pull request and release.
```yaml
---
- name: Converge
  hosts: all
  become: true

  pre_tasks:
    - name: Update apt cache.
      ansible.builtin.package:
        update_cache: true
        cache_valid_time: 600
      when: ansible_os_family == 'Debian'

    - name: Ensure build dependencies are installed (RedHat).
      ansible.builtin.package:
        name:
          - openssh-server
          - openssh-clients
        state: present
      when: ansible_os_family == 'RedHat'

    - name: Ensure build dependencies are installed (Fedora).
      ansible.builtin.package:
        name: procps
        state: present
      when: ansible_distribution == 'Fedora'

    - name: Ensure build dependencies are installed (Debian).
      ansible.builtin.package:
        name:
          - openssh-server
          - openssh-client
        state: present
      when: ansible_os_family == 'Debian'

    - name: Ensure auth.log file is present.
      ansible.builtin.copy:
        dest: /var/log/auth.log
        content: ""
        force: false
        mode: 0644
      when: ansible_distribution == 'Debian'

  roles:
    - role: geerlingguy.security
```


## [Role Variables](#role-variables)

The default values for the variables are set in `defaults/main.yml`:
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

security_autoupdate_enabled: true
security_autoupdate_blacklist: []

# Autoupdate mail settings used on Debian/Ubuntu only.
security_autoupdate_reboot: "false"
security_autoupdate_reboot_time: "03:00"
security_autoupdate_mail_to: ""
security_autoupdate_mail_on_error: true

security_fail2ban_enabled: true
security_fail2ban_custom_configuration_template: "jail.local.j2"
```

## [Requirements](#requirements)

- pip packages listed in [requirements.txt](https://github.com/buluma/ansible-role-security/blob/main/requirements.txt).


## [Context](#context)

This role is a part of many compatible roles. Have a look at [the documentation of these roles](https://buluma.co.ke/) for further information.

Here is an overview of related roles:

![dependencies](https://raw.githubusercontent.com/buluma/ansible-role-security/png/requirements.png "Dependencies")

## [Compatibility](#compatibility)

This role has been tested on these [container images](https://hub.docker.com/u/buluma):

|container|tags|
|---------|----|
|el|all|
|fedora|all|
|debian|all|
|ubuntu|all|

The minimum version of Ansible required is 2.4, tests have been done to:

- The previous version.
- The current version.
- The development version.



If you find issues, please register them in [GitHub](https://github.com/buluma/ansible-role-security/issues)

## [License](#license)

Apache-2.0

## [Author Information](#author-information)

[Michael Buluma](https://buluma.github.io/)
