Gitlab installation
=========
[![License](https://img.shields.io/badge/license-Apache-green.svg?style=flat)](https://raw.githubusercontent.com/lean-delivery/ansible-role-gitlab/master/LICENSE)
[![Build Status](https://travis-ci.org/lean-delivery/ansible-role-gitlab.svg?branch=master)](https://travis-ci.org/lean-delivery/ansible-role-gitlab)
[![Build Status](https://gitlab.com/lean-delivery/ansible-role-gitlab/badges/master/build.svg)](https://gitlab.com/lean-delivery/ansible-role-gitlab/pipelines)
[![Galaxy](https://img.shields.io/badge/galaxy-lean__delivery.gitlab-blue.svg)](https://galaxy.ansible.com/lean_delivery/gitlab)
![Ansible](https://img.shields.io/ansible/role/d/29896.svg)
![Ansible](https://img.shields.io/badge/dynamic/json.svg?label=min_ansible_version&url=https%3A%2F%2Fgalaxy.ansible.com%2Fapi%2Fv1%2Froles%2F29896%2F&query=$.min_ansible_version)
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
 - **Mysql 5.6 and later installed if Gitlab EE installed and parameter set** [![Build Status](https://travis-ci.org/lean-delivery/ansible-role-mysql.svg?branch=master)](https://travis-ci.org/lean-delivery/ansible-role-mysql)
 - **Supported OS**:
   - CentOS
     - 7
   - Ubuntu
   - Debian

## Role Variables
--------------
  - `host_fqdn` - host FQDN  
     default: `{{ ansible_fqdn }}`
  - `gitlab_install` - to install gitlab; already installed gitlab could be used for configuration  
     default: `true`
  - `gitlab_external_url` - Gitlab external url  
     default: `https://{{ host_fqdn }}`
  - `gitlab_data_dir` - Gitlab custom directory with data  
     default: `/var/opt/gitlab/git-data`
  - `gitlab_edition` - Gitlab edition. ee or ce  
     default: `ce`
  - `gitlab_version` - Gitlab version  
     default: `latest`
  - `gitlab_api_version` - Gitlab api version; v4 for version 9.0 and later; if Gitlab is installed by the role this variable reset  
     default: `v4`
# gitlab super admin user parameters. User will be created during installation.
  - `gitlab_admin_email` - admin email address  
     default: `superdamin@example.com`
  - `gitlab_admin_name` - admin name  
     default: `Administrator`
  - `gitlab_admin_username` - admin username  
     default: `superdamin`
  - `gitlab_admin_password` - admin password  
     default: `Qwe54321`
  - `gitlab_admin_token` - admin api token  
     default: `BF1U1swzaouACMj2S9aQ`
# gitlab ssl parameters
  - `gitlab_ssl_redirect_http_to_https` - enable https redirection  
     default: `true`
  - `gitlab_ssl_certificate_path` - path to public cert  
     default: `/etc/gitlab/ssl/gitlab.crt`
  - `gitlab_ssl_certificate_key_path` - path to private cert  
     default: `/etc/gitlab/ssl/gitlab.key`
  - `gitlab_ssl_create_self_signed_cert` - to create self signed cert
     default: `true`
  - `gitlab_ssl_self_signed_cert_subj` - self signed cert subj  
     default: `/C=BY/ST=Minsk/L=org/O=IT/OU=IT/CN={{ host_fqdn }}`
# ldap configuration for gitlab
  - `gitlab_ldap_enabled` - enable ldap usage  
     default: `false`
  - `gitlab_ldap_host` - ldap server name  
     default: `example.com`
  - `gitlab_ldap_port` - ldap server port  
     default: `389`
  - `gitlab_ldap_uid` -
     default: `sAMAccountName`
  - `gitlab_ldap_method` -  
     default: `plain`
  - `gitlab_ldap_bind_dn` -  
     default: `CN=Username,CN=Users,DC=example,DC=com`
  - `gitlab_ldap_password` -  
     default: `password`
  - `gitlab_ldap_base` -  
     default: `DC=example,DC=com`
# gitlab configuration
  - `gitlab_config_time_zone` - time zone  
     default: `UTC`
  - `gitlab_config_backup_keep_time` - backup retention time  
     default: `604800`
# mail configuration
  - `gitlab_email_enabled` - enable mail send configuration  
     default: `false`
  - `gitlab_email_from` - from address  
     default: `gitlab@example.com`
  - `gitlab_email_display_name` - from display  
     default: `Gitlab`
  - `gitlab_email_reply_to` - reply to address  
     default: `gitlab@example.com`
# mysql usage. For EE only!
  - `gitlab_mysql_enabled` - mysql usage enable  
     default: `false`
  - `gitlab_mysql_db_adapter` - db adapter  
     default: `mysql2`
  - `gitlab_mysql_db_encoding` - db encoding  
     default: `utf8`
  - `gitlab_mysql_db_host` - db server name  
     default: `localhost`
  - `gitlab_mysql_db_port` - d server port  
     default: `3306`
  - `gitlab_mysql_db_username` - user name  
     default: `USERNAME`
  - `gitlab_mysql_db_password` - user password  
     default: `PASSWORD`
# smtp settings
  - `gitlab_smtp_enabled` - to enable smtp  
     default: `false`
  - `gitlab_smtp_address` -  
     default: `smtp.gmail.com`
  - `gitlab_smtp_port` -  
     default: `587`
  - `gitlab_smtp_user_name` -  
     default: `my.email@gmail.com`
  - `gitlab_smtp_password` -  
     default: `my-gmail-password`
  - `gitlab_smtp_domain` -  
     default: `smtp.gmail.com`
  - `gitlab_smtp_authentication` -  
     default: `login`
  - `gitlab_smtp_enable_starttls_auto` -  
     default: `true`
  - `gitlab_smtp_tls` -  
     default: `false`
  - `gitlab_smtp_openssl_verify_mode` -  
     default: `peer`

  - `gitlab_validate_certs` - to validate SSL certificate during API call  
     default: `false`

# gitlab group creation/configuration
  - `gitlab_project_group_create` - to create gitlab group; correct gitlab_admin_token should be set if gitlab not installed by this role  
     default: `false`
  - `gitlab_project_group` - group name  
     default: `test_group`
  - `gitlab_project_group_id` - group id; should be set if group creation is false  
     default: `1`
# gitlab project creation/configuration
  - `gitlab_project_create` - to create gitlab project; correct gitlab_admin_token should be set if gitlab not installed by this role  
     default: `false`
  - `gitlab_project_name` - project name  
     default: `test_project`
  - `gitlab_project_id` - project id; should be set if project creation is false  
     default: `1`
# master user creation/configuration
  - `gitlab_master_user_create` - to create gitlab project master user; correct gitlab_admin_token should be set if gitlab not installed by this role  
     default: `false`
  - `gitlab_master_name` - user name  
     default: `integrator user`
  - `gitlab_master_username` - username  
     default: `integrator`
  - `gitlab_master_password` - user password  
     default: `Admin!23`
  - `gitlab_master_email` - user email  
     default: `admin@example.com`
  - `gitlab_master_token_name` - name for user private api token  
     default: `Created API token`
  - `gitlab_master_token` - user token; will be created if name not exists; does not visible for user; reset variable after creation; ***Should be set manually for versions earlier than 9.0***  
     default: `Token!234`
# webhooks creation
  - `gitlab_webhooks_create` - to create webhooks; correct gitlab_admin_token should be set if gitlab not installed by this role  
     default: `false`
  - `gitlab_webhooks_list` - map with webhooks parameters  
  - `gitlab_allow_local_requests` - enable the option [“Allow requests to the local network from hooks and services”](https://docs.gitlab.com/ee/security/webhooks.html) in the “Outbound requests” section  
     default: `false`
    ```
    webhook1:
      hook_url: "http://server.example.com:8080/project/ci_main_branch_test"
      push_events: "true"
      push_events_branch_filter: ""
      issues_events: "false"
      confidential_issues_events: "false"
      merge_requests_events: "false"
      tag_push_events: "false"
      note_events: "false"
      job_events: "false"
      pipeline_events: "false"
      wiki_page_events: "false"
      enable_ssl_verification: "false"
      token: ""
    ```
# labels creation
  - `gitlab_labels_create` - to create labels; correct gitlab_admin_token should be set if gitlab not installed by this role  
     default: `false`
  - `gitlab_labels_list` - map with labels parameters  
     ```
     label1:
       name: 'Skip Deploy'
       color: '#34495E'
       description: ''
     ```

# nginx configuration
  - `gitlab_nginx_listen_port` -  
     default: ``
  - `gitlab_nginx_listen_https` -  
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
    - role: lean_delivery.gitlab
```

Note. For local test in docker 
----------------
Insert this task in ansible-role-gitlab\tasks\install.yml before "Reconfigure GitLab (first run)."
```yml
- name: "Task on CI issue"
  shell: nohup /opt/gitlab/embedded/bin/runsvdir-start </dev/null >/dev/null 2>&1 &
  args:
    executable: "/bin/bash"
    removes: /usr/bin/gitlab-ctl
  changed_when: false
```

License
-------

Apache

Author Information
------------------

authors:
  - Lean Delivery Team <team@lean-delivery.com>
