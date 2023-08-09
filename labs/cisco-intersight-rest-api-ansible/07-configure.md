## Configure settings via Meraki Dashboard API

Now that we have successfully fetched information using Ansible, we can make configuration changes.

### Changing a VLAN assignment to a switch port

The following playbook with associate port 1 on switch AAAA-BBBB-CCCC with VLAN 10.

```
---
- hosts: meraki_servers
  gather_facts: false
  tasks:
    - name: update ports
      cisco.meraki.devices_switch_ports:
        meraki_suppress_logging: true
        state: present
        serial: "AAAA-BBBB-CCCC"
        vlan: 10
        portId: 1
```

The next playbook will configure SSID #0 on Network ID "L_12341234" as "ACME" with WPA-PSK (with a super secret password :-)) tagged to VLAN 100. 

```
---

- hosts: meraki_servers
  vars:
    corp_name: "ACME"
    network_id: "L_12341234"
  gather_facts: false
  tasks:

    - name: Create WPA-PSK SSID
      cisco.meraki.networks_wireless_ssids:
        state: present
        enabled: true
        name: "{{corp_name}}1"
        networkId: "{{ network_id }}"
        number: "0"
        ipAssignmentMode: Bridge mode
        defaultVlanId: 100
        useVlanTagging: true
        authMode: psk
        encryptionMode: wpa
        psk: SuperSecretPreSharedKey
```