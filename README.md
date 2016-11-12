Ansible Role for SFTP [![Build Status](https://travis-ci.org/StalkingKillah/ansible-role-sftp.svg?branch=master)](https://travis-ci.org/StalkingKillah/ansible-role-sftp)
=========

Role for setting up SFTP access.

Requirements
------------

No pre-requisites.

Role Variables
--------------

* sftp_group_name - name of the user group allowed to login via SFTP (default: sftp-users)
* sftp_user_home_tld - top level home directory in which user home directories are to be created (default: /home)
* sftp_user_shell - default shell for created users. (default: /sbin/nologin)
* sftp_allow_passwords - should password logins be allowed. (default: no)
* sftp_additional_directories - list of additional directories (can be a dictionary with defined fields: name, mode) to be created at the end of the role. (default: [])
* sftp_users - list of dictionaries with defined fields: name (username), password (should be hashed), key (authorized ssh key, string)

Dependencies
------------

No dependencies.

Example Playbook
----------------

If role is pulled from github, role name should be ansible-role-sftp.
If role is installed from ansible galaxy, role name should be StalkingKillah.sftp

    - hosts: all
      remote_user: root
      vars:
        - users:
          - name: "sftptestuser1"
            password: "{{ 'THISROCKS' | password_hash('sha512') }}"
      roles:
        - role: StalkingKillah.sftp
          sftp_users: "{{ users }}"
          sftp_additional_directories:
            - test1
            - test2
            - test3

License
-------

MIT

Author Information
------------------

Author: Djordje Stojanovic
