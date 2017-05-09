Role Name
=========

This role is supposed to get Let's Encrypt certificates for listed domains (using the [ansible letsencrypt module](https://docs.ansible.com/ansible/letsencrypt_module.html)) 

Requirements
------------

As a pre-requisite you need to have installed nginx or some other webserver

Role Variables
--------------

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

```
letsencrypt_domains: []

letsencrypt_cert_base_path: /etc/pki/cert
letsencrypt_certificate_path: /etc/nginx/ssl
letsencrypt_challenge_public_path: /var/www/html/

letsencrypt_account_key_path: '{{ letsencrypt_cert_base_path }}/private/account.key'
letsencrypt_domain_csr_path: '{{ letsencrypt_cert_base_path }}/{{ letsencrypt_domains[0] }}.csr'
letsencrypt_valid_certificate_path: '{{ letsencrypt_cert_base_path }}/{{ letsencrypt_domains[0] }}.crt'

# Final generated private key and certificate.
letsencrypt_domain_key_path: '{{ letsencrypt_certificate_path }}/{{ letsencrypt_domains[0] }}.key'
letsencrypt_chained_pem_path: '{{ letsencrypt_certificate_path }}/{{ letsencrypt_domains[0] }}.pem'

# For production, set this to:
#   letsencrypt_default_ca: 'https://acme-v01.api.letsencrypt.org'
letsencrypt_default_ca: 'https://acme-staging.api.letsencrypt.org'

# How often should we try to renew certificates? Default is once per month.
letsencrypt_cron_renew: ['0', '0', '*/3', '*', '*']

```

Dependencies
------------

[geerlingguy.certbot](https://github.com/geerlingguy/ansible-role-certbot) for adding cronjob to renew certs

<!-- Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 } -->

License
-------

BSD, MIT
