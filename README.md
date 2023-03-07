<h1 align="center">
  Installing Hive Fabric On phoenixNAP BMC
</h1>

<p>Ansible playbooks for installing Hive Fabric on a BMC server 
based on <a href="https://github.com/phoenixnap/ansible-ramos-bmc">phoenixnap/ansible-ramos-bmc</a></p>

## Requirements

- [Bare Metal Cloud](https://bmc.phoenixnap.com) account
- Ansible 2.9+
- Python 2 (version 2.7) or Python 3 (versions 3.5 and higher)
  - Python **_requests_** package

## Installing Ansible

Follow these helpful tutorials to learn how to install Ansible on Ubuntu and Windows machines.

- [How to Install and Configure Ansible on Ubuntu 20.04](https://phoenixnap.com/kb/install-ansible-ubuntu-20-04)
- [How to Install and Configure Ansible on Windows](https://phoenixnap.com/kb/install-ansible-on-windows)

## Installing the Bare Metal Cloud Ansible module

This Ansible collection contains the **_server_** module which requires the Python **_requests_** HTTP library to work properly. If you don't have it installed on your machine already, run this command to install it:

    pip install requests

Now install the Ansible collection by running:

    ansible-galaxy collection install phoenixnap.bmc

## Authentication

You need to create a configuration file called `config.yaml` and save it in the user home directory. This file is used to authenticate access to your Bare Metal Cloud resources.

In your home directory, create a folder `.pnap` and a `config.yaml` file inside it.

This file needs to contain only two lines of code:

    clientId: <enter your client id>
    clientSecret: <enter your client secret>

To get the values for the clientId and clientSecret, follow these steps:

1. [Log in to the Bare Metal Cloud portal](https://bmc.phoenixnap.com).
2. On the left side menu, click on API Credentials.
3. Click the Create Credentials button.
4. Fill in the Name and Description fields, select the permissions scope and click Create.
5. In the table, click on Actions and select View Credentials from the dropdown.
6. Copy the values from the Client ID and Client Secret fields into your `config.yaml` file.

## Ansible Playbooks

The Ansible Playbook allows you to provision and install hive-fabric on a Bare Metal Cloud server.
* **_inventory.yaml_** contains all the information about the BMC server.
* **_provision.yaml_** deploys the BMC server using the RAM OS feature. The playbook uses the information from **_inventory.yaml_**

The defaults will use a **d2.c2.large** server in **Phoenix** at an **hourly rate**

to deploy and install fabric run:

    
    ANSIBLE_HOST_KEY_CHECKING=False ansible-playbook provision.yaml -i inventory.yaml


to destroy the server:

    ANSIBLE_HOST_KEY_CHECKING=False ansible-playbook destroy.yaml -i inventory.yaml

