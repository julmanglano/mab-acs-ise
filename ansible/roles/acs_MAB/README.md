Role acs_MAB
=========

This role is for adding (only adding ) MAB devices to the ACS
The MACs are added on the IDGROUP files that are under host_vars/kbh-acs.schibsted.se/

For adding a new MAC address the id has to be 0 ( as per the ACS API requirements)

For example, if we want to add a new MAC address on the group 1028_OFFICE-PLAYIPP, we have to add the MAC on the yml file for that group

The format is as it follows:

- mac: 6c-21-a2-18-be-31
  description: "MPC Cognition sk1"
  enabled: true
  idgroup: 1028_OFFICE-PLAYIPP
  id: 0


The idgroup must exist on the IDGROUPS.yml file, so if a new group is created must be added to that file as well.

After adding the MAC to the ACS, the role will update the ISE files so there is consistency with the MACs that are present on both devices.

After adding the MAC the playbook will call the role replace_MAB_id to change the id of the newly added MACs with a random number in order to avoid errors and to save us of doing this manually.
This role is available for both acs_MAB and ise_MAB roles.



Requirements
------------

Any pre-requisites that may not be covered by Ansible itself or the role should be mentioned here. For instance, if the role uses the EC2 module, it may be a good idea to mention in this section that the boto package is required.

Role Variables
--------------

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: servers
      roles:
         - { role: username.rolename, x: 42 }

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
