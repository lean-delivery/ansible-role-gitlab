Gitlab installation
=========
[![License](https://img.shields.io/badge/license-Apache-green.svg?style=flat)](https://raw.githubusercontent.com/lean-delivery/ansible-role-gitlab/master/LICENSE)
[![Build Status](https://travis-ci.org/lean-delivery/ansible-role-gitlab.svg?branch=master)](https://travis-ci.org/lean-delivery/ansible-role-gitlab)
## Summary

This role:
  - Installs Gitlab on Ununtu and Centos7
  - Configures Gitlab
  
Role tasks
------------
  - Install Gitlab
  - Configure Gitlab
  
Requirements
------------

 - Minimal Version of the ansible for installation: 2.5
 - **Mysql 5.6 and later installed if Gitlab EE installed and parameter set** [![Build Status](https://travis-ci.org/lean-delivery/ansible-role-mysql.svg?branch=master)](https://travis-ci.org/lean-delivery/ansible-role-mtsql)
 - **Supported OS**:
   - CentOS
     - 7
   - Ubuntu
   
## Role Variables
--------------	
  - `gitlab` - configuration for gitlab
    - `external_url` - Gitlab external url
       default: `https://{{ ansible_fqdn }}`
    - `git_data_dir` - Gitlab custom directory with data
       default: `/var/opt/gitlab/git-data`
    - `edition` - Gitlab edition. ee or ce
       default: `ce`
    - `version` - Gitlab version
       default: `latest`
  - `gitlab_admin` - gitlab super admin user parameters. User will be created during installation.
    - `email` - admin email address
       default: `superdamin@example.com`
    - `name` - admin name
       default: `Administrator`
    - `username` - admin username
       default: `superdamin`
    - `password` - admin password
       default: `Qwe54321`
    - `token` - admin api token
       default: `BF1U1swzaouACMj2S9aQ`
  - `gitlab_ssl` - gitlab ssl parameters
    - `redirect_http_to_https` - enable https redirection
       default: `True`
    - `certificate_path` - path to public cert
       default: `/etc/gitlab/ssl/gitlab.crt`
    - `certificate_key_path` - path to private cert
       default: `/etc/gitlab/ssl/gitlab.key`
    - `create_self_signed_cert` - to create self signed cert
       default: `True`
    - `self_signed_cert_subj` - self signed cert subj
       default: `/C=BY/ST=Minsk/L=org/O=IT/OU=IT/CN={{ ansible_fqdn }}`
  - `gitlab_ldap` - ldap configuration for gitlab
    - `enabled` - enable ldap usage
       default: `False`
    - `host` - ldap server name
       default: `example.com`
    - `port` - ldap server port
       default: `389`
    - `uid` - 
       default: `sAMAccountName`
    - `method` - 
       default: `plain`
    - `bind_dn` - 
       default: `CN=Username,CN=Users,DC=example,DC=com`
    - `password` - 
       default: `password`
    - `base` - 
       default: `DC=example,DC=com`
  - `gitlab_config` - gitlab configuration
    - `time_zone` - time zone
       default: `America/New_York`
    - `backup_keep_time` - backup retention time
       default: `604800`
  - `gitlab_email` - mail configuration
    - `enabled` - enable mail send configuration
       default: `False`
    - `from` - from address
       default: `gitlab@example.com`
    - `display_name` - from display 
       default: `Gitlab`
    - `reply_to` - reply to address
       default: `gitlab@example.com`
  - `gitlab_mysql` - mysql usage. For EE only!
    - `enabled` - mysql usage enable
       default: `False`
    - `db_adapter` - db adapter
       default: `mysql2`
    - `db_encoding` - db encoding
       default: `utf8`
    - `db_host` - db server name
       default: `localhost`
    - `db_port` - d server port
       default: `3306`
    - `db_username` - user name
       default: `USERNAME`
    - `db_password` - user password
       default: `PASSWORD`
  - `gitlab_smtp` - 
    - `enabled` - 
       default: `False`
    - `address` - 
       default: `smtp.gmail.com`
    - `port` - 
       default: `587`
    - `user_name` - 
       default: `my.email@gmail.com`
    - `password` - 
       default: `my-gmail-password`
    - `domain` - 
       default: `smtp.gmail.com`
    - `authentication` - 
       default: `login`
    - `enable_starttls_auto` - 
       default: `true`
    - `tls` - 
       default: `false`
    - `openssl_verify_mode` - 
       default: `peer`
  - `gitlab_nginx` - 
    - `listen_port` - 
       default: ``
    - `listen_https` - 
       default: ``

Example Inventory
----------------
[gitlab]
server.example.com

Example Playbook
----------------

```yml
- name: Install and Configure Gitlab
  hosts: gitlab
  roles:
    - role: lean-delivery.gitlab
```

License
-------

Apache2

Author Information
------------------

DEP Infrastructure Platform
