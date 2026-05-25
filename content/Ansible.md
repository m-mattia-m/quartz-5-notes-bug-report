---
publish: true
created: 2026-01-29T21:35:21.000+01:00
modified: 2026-02-16T21:59:13.987+01:00
tags:
  - Tech/Ansible
---

# What is Ansible?

Ansible is an automation tool which allows you to automate a complete infrastructure. You have one controller node (can also be the client) from which you manage the whole infrastructure. You can set everything up in the same way, update it automatically (with zero downtime), etc. The control node then connects via SSH to the other nodes. The advantage is that you only need to create a new node, but you don’t have to configure anything manually, because this is handled by Ansible. For Ansible you only write playbooks (YAML configurations) which define how the nodes should be set up.

# Installation

Install Ansible CLI on the controller node

> `pip install ansible`
> `brew install ansible`

# New Node

All inventory nodes are stored in the `root` folder inside the `inventory.ini` file. Add all hostnames or FQDNs in this file.

Check if the inventory is correct with: `ansible-inventory -i inventory.ini --list`

# Setup

## Directory structure

You can also add your own environments like dev or test.

[Best Practices — Ansible Documentation](https://docs.ansible.com/ansible/2.8/user_guide/playbooks_best_practices.html#alternative-directory-layout)
