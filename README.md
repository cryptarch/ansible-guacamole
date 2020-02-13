# Ansible playbook to set up Guacamole

This project includes scripts and an Ansible playbook to set up [Apache Guacamole](https://guacamole.apache.org/), with some pre-configuration for Let's Encrypt included.

It started as a fork of the [NeCTAR Research Cloud's RStudio packer image](https://github.com/NeCTAR-RC/packer-rstudio), with the RStudio elements removed.

It is under an Apache licence; see [`LICENSE.md`](./LICENSE.md) for more information.

Usage
----

Set up the target host in your Ansible inventory (`/etc/ansible/hosts`) with a stanza like so:

```
[cloud]
<ip-address>
```

Then run `ansible-playbook playbook.yml` under the `./ansible` directory.

It is set up to permit login by users in the `rdp` group.

More detailed instructions
----

**Motivation:** This playbook was prepared with the idea of setting up a golden image for workshops focused on introducing cloud computing.
The following notes are copied from a message about how to do such a setup.

Setting up guacamole and xfce the first time take a lot of time to download and install everything.
You don't want to have to do that 20 times for every workshop.
So, the idea is to set all that up once on a throw-away instance, then power it down and snapshot it, and later use the snapshot for all the instances you create before a workshop.

To use this repo to create that golden image:

1. Install ansible on your admin box (check `./scripts/ansible.sh` for how to do that), and clone the ansible-guacamole repo onto the admin box.
2. Set up another Ubuntu 18.04 instance which will be used as the basis for a golden image.
   Note its IP address.
   You will need it for the next step, when setting up the "inventory" so ansible knows which servers to talk to.
3. Look above under Usage for how to create the inventory.
   For the present use case, it is just a couple of lines in `/etc/ansible/hosts`.
   (You might wonder why the inventory stanza is called `[cloud]`.
   No special reason.
   It is an arbitrary choice, so long as you update the hosts field in `playbook.yml` to match it.)
4. Go into the ansible sub-directory in this repo and run `ansible-playbook playbook.yml`
5. If that completes successfully, power the instance down and create an instance snapshot.
