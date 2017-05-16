GitLab
======
Install and configure GitLab Community Edition (CE) through the Omnibus package.

This role adds the official repository, but leaves it disabled.

Requirements
------------
See `meta/main.yml`.

Role Variables
--------------
See `defaults/main.yml` for all options. Following are a few notes:

`gitlab_version` specifies the GitLab version to install. Each version of GitLab might need a different `gitlab.rb.j2` template and variables to support upstream new features and changes. Therefore, if you need an earlier version you should checkout the corresponding commit to get the matching `gitlab.rb.j2` template and variables.

LDAP can be enabled by setting `gitlab_ldap_enabled: true` and configuring `gitlab_ldap_` variables to match your setup. Take a look at the `templates/gitlab.rb.j2` for how ldap is configured or the GitLab documentation for more detailed instructions.

By default nginx won't redirect http to https. Set `gitlab_nginx_redirect_http_to_https: true` to activate this feature and then set the key/pair certificate locations using `gitlab_nginx_ssl_certificate` and `gitlab_nginx_ssl_certificate_key`. This variables point to the location of key/cert files in the target system, you need some way to get those files there, i.e. using a role `jdauphant.ssl-certs`.

Backup of Gitlab's application data, secrets and config can be enabled in `gitlab_backup_enabled` (disabled by default). When enabled, backups are made daily and kept for 7 days (tweak values in `gitlab_backup_frequency` and `gitlab_backup_keep_time`). Backups are performed in two cron jobs and saved in the standard gitlab backup directory (`/var/opt/gitlab/backup`):
- Application data is performed by Gitlab's rake task `gitlab:backup:create` and archived in `timestamp_gitlab_backup.tar`.
- Gitlab configuration in `/etc/gitlab` (including `gitlab-secrets.json`) and ssh host keys are archived  `timestamp_gitlab_config.tar`.

Note that secrets backups are currently stored in the same directory as the application data.

Dependencies
------------
None.

Example Playbook
----------------
Example:
```
- hosts: servers
  roles:
    - gitlab
```

TODO
----
- Activate `repo_gpgcheck`. Rpm from repository is not signed, but the repo itself is, however yum gets into validation problems of the repo.

Licence
-------
Licensed under [CC-BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/).

Author Information
------------------
Luis Gracia <luis.gracia@ebi.ac.uk> [luisico](https://github.com/luisico)
