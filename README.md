User-Management
=========

This role deploys the management user account on my newly created virtual machine. It also deploys ssh-keys for connections. This user account (and these keys) is used by ansible for future playbooks and tasks. 

Requirements
------------

This playbook assumes there is a default provisioned user on the machine that can be logged into using the provided username and password. This default user must have sudo privileges. 

Role Variables
--------------
Required variables are listed here, along with default example values. See defaults/main.yml.

    management_user: username

This is the user to be deployed on the system. 

    management_pass: pass

This is the password that will be associated with the new user. This should not be plain text as this example shows, instead it should be presented and stored in a more secure manner, like ansible vault.

    provisioned_user:

This is the user that should already be present on the system. Ansible will use this user to connect for the first time. 

    provisioned_pass:

This is the password that ansible uses to connect to the system for the first time. Once again, I do not recommend using plain text to store this variable.

Dependencies
------------

None

Example Playbook
----------------

    - name: Add the ansible management user.
      hosts: linux
      gather_facts: false
      remote_user: "{{ provisioned_user }}"
      become: true
      vars_files:
        - roles/user-management/vars/vault
      vars:
        ansible_become_pass: "{{ provisioned_pass }}"
        ansible_ssh_pass: "{{ provisioned_pass }}"
      roles:
        - role: user-management

This playbook creates the management user on my new virtual machines. Instead of passing through passwords in plain text (like the defaults above), this utilizes an ansible vault file located at roles/user-management/vars/vault.

License
-------

BSD

Author Information
------------------

Derek Smiley - Network Analyst, avid Homelabber, and aspiring System Administrator/Ansible Automation Engineer. 

Connect with me on LinkedIn - https://www.linkedin.com/in/derek-smiley/

Much of this was created using snippets from other public repositories on github. I claim ownership of none of this code.