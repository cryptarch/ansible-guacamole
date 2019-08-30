# Ansible playbook to set up Guacamole

This project includes scripts and an Ansible playbook to set up [Apache Guacamole](https://guacamole.apache.org/), with some pre-configuration for Let's Encrypt included.

It started as a fork of the [NeCTAR Research Cloud's RStudio packer image](https://github.com/NeCTAR-RC/packer-rstudio), with the RStudio elements removed.

Usage
----

Set up the target host in your Ansible inventory (`/etc/ansible/hosts`) with a stanza like so:

```
[cloud]
<ip-address>
```

Then run `ansible-playbook playbook.yml` under the `./ansible` directory.

It is set up to permit login by users in the `rdp` group.
