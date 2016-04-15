GitLab
======
Install and configure GitLab Community Edition (CE) through the Omnibus package.

This role adds the official gitlab repository, but leaves it disabled.

Requirements
------------
See `meta/main.yml`.

Role Variables
--------------
See `defaults/main.yml`.

To enable ldap authentication, set `gitlab_ldap_enabled: true` and configure the rest of `gitlab_ldap_` variables for your setup (see `default/main.yml`). Take a look at the `templates/gitlab.rb.j2` for how ldap is configured or the GitLab documentation for more detailed instructions.

By default nginx won't redirect http to https. Set `gitlab_nginx_redirect_http_to_https: true` to activate this feature and then set the key/pair certificate locations using `gitlab_nginx_ssl_certificate` and `gitlab_nginx_ssl_certificate_key`. This variables point to the location of key/cert files in the target system, you need some way to get those files there, i.e. using a role `jdauphant.ssl-certs`.

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
- Select gitlab version to install.

Licence
-------
Licensed under [CC-BY-SA 4.0](https://creativecommons.org/licenses/by-sa/4.0/).

Author Information
------------------
Luis Gracia <luis.gracia@ebi.ac.uk>