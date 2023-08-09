## Ansible Collection Help and Query Examples

Now that you have API authentication configured, you can run example playbooks that query Meraki's Dashboard API. To view examples, change directory to the playbooks subdirectory that was installed with the Collection.

```bash
cd /home/developer/.ansible/collections/ansible_collections/cisco/meraki/playbooks
```

### Query the API for data

Meraki's Dashboard API can be used to query various information. For example, list all of the organizations the API key has access to (equivalent to [this API endpoint](https://developer.cisco.com/meraki/api-v1/get-organizations/) and):

```
---
- hosts: meraki_servers
  gather_facts: false
  tasks:
    - name: Get all Organizations
      cisco.meraki.organizations_info:
      register: result

    - name: Show result
      ansible.builtin.debug:
        msg: "{{ result }}"
```
Note the play had two tasks:
1. Retrieve the organization list via Dashboard API.
2. Print the result to the screen.

Another example is fetching all of the devices in your organization's inventory:
```
---
- hosts: meraki_servers
  gather_facts: false
  tasks:
    - name: Get Device
      cisco.meraki.devices_info:
        meraki_suppress_logging: true
        organizationId: 123123123 # replace with your organization ID
      register: result

    - name: Show result
      ansible.builtin.debug:
        msg: "{{ result }}"
```