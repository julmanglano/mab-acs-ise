# mab-acs-ise

There are three playbooks included in this repository for managing MAB entries in both ACS and ISE


## acs_MAB.yml
It can be used **only** for adding entries to the ACS
The variables are located in 
```
ansible/playbooks/host_vars/kbh-acs.schibsted.se
```
There, you can find the API_CREDENTIALS, vault encrypted, the list of IDGROUPS and a yml file per each IDGROUP,
the new entries are added on these files with the following format:

```
- mac: 00-22-FB-3A-87-F8
  description: "no description"
  enabled: true
  idgroup: 1900_LAN_Omni
  id: 0
```
For adding a new MAC the id has to be ***0***

The playbook will push this new entry (or entries) to the ACS.
After that is done, it will copy all the variable files to the ISE directory, so these
new entries can be added afterwards to the ISE. This logic is implemented with the upcoming 
migration to the ISE in mind, so the data is kept consistent.
After that, it will update the modified variable file to change the id 0 
for the newly added MACs with a random number so the next time you run the playbook
it won't try to push an old mac.

For running the playbook:

```
ansible-playbook -i hosts playbooks/acs_MAB.yml --ask-vault-pass
```

## ise_MAB.yml

This playbook can be used for adding or updating MAB entries on the ISE
The variables are located at:

```
ansible/playbooks/host_vars/c524pa-1-ise.schibsted.se
```

And the data structure is identical to the one for ACS

The logic is the same as for the previous playbook, for adding a new MAC the id has to be 0
For modifying an existing MAC (change description, move to a different IDGROUP), again id 0

```
- mac: 18-65-71-5E-B2-BF
  description: "Entrance Floor 7 SW"
  enabled: true
  idgroup: 1028_OFFICE-PLAYIPP
  id: 0
```

Again if you add or modify a MAC entry, the playbook will update the variables file to swap the id 0
for a random one.

For running the playbook:

```
ansible-playbook -i hosts playbooks/ise_MAB.yml --ask-vault-pass
```

## ise_delete_MAB.yml

This one can be used for removing MAC entries, for that id has to be -1

```
- mac: 18-65-71-5E-B2-BF
  description: "Entrance Floor 7 SW"
  enabled: true
  idgroup: 1028_OFFICE-PLAYIPP
  id: -1
```

Once a MAC is deleted from the ISE, the playbook will swap the id -1 for the word deleted on the variables files

For running the playbook:

```
ansible-playbook -i hosts playbooks/ise_delete_MAB.yml --ask-vault-pass
```














