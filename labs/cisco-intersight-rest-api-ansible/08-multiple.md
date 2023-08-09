## Performing multiple operations

Ansible allows us to iterate over multiple values, just like `for` and `while` loops in other programming languages.
In the following example, we will iterate over all networks configured in an organization, and configure 3 different wireless SSIDs in each network that has wireless APs.
1. A corporate SSID (with 802.1x) on vlan 100.
2. A mobile SSID (with WPA-PSK) on vlan 200.
3. A guests SSID (with a captive portal) on vlan 300.


```
---
- hosts: meraki_servers
  vars:
    org_id: "123123123"
    corp_name: "ABC Corp"
  gather_facts: false
  tasks:

    - name: Get Organization Networks
      cisco.meraki.networks_info:
        organizationId: "{{ org_id }}"
      register: result

    - name: Filter networks with "wireless" productTypes
      set_fact:
        filtered_networks: "{{ result.meraki_response | selectattr('productTypes', 'contains', 'wireless') | list }}"

    - name: Create corporate SSID
      cisco.meraki.networks_wireless_ssids:
        state: present
        enabled: true
        name: "{{corp_name}}"
        networkId: "{{ item.id }}"
        number: 1
        ipAssignmentMode: Bridge mode
        defaultVlanId: 100
        useVlanTagging: true
        authMode: "8021x-radius"
        radiusServers: 
          - one:
            host: "1.2.3.4"
            port: 1812
            secret: SuperSecretPassword

      loop: "{{ filtered_networks }}"
      loop_control:
        label: "{{ item.id }}"

    - name: Create Mobile/PSK SSID
      cisco.meraki.networks_wireless_ssids:
        state: present
        enabled: true
        name: "{{corp_name}}-legacy"
        networkId: "{{ item.id }}"
        number: 2
        ipAssignmentMode: Bridge mode
        defaultVlanId: 200
        useVlanTagging: true
        authMode: psk
        encryptionMode: wpa
        psk: SuperSecretPreSharedKey

      loop: "{{ filtered_networks }}"
      loop_control:
        label: "{{ item.id }}"

    - name: Create Guest SSID
      cisco.meraki.networks_wireless_ssids:
        state: present
        enabled: true
        name: "{{corp_name}}-Guests"
        networkId: "{{ item.id }}"
        number: 3
        ipAssignmentMode: Bridge mode
        defaultVlanId: 300
        useVlanTagging: true
        authMode: "open"
        splashPage: Click-through splash page

      loop: "{{ filtered_networks }}"
      loop_control:
        label: "{{ item.id }}"
```

The first task `Get Organization Networks`, returns a list of networks in the organization.
Then, the second task `Filter networks with "wireless" productTypes` returns a filtered list of networks that have "wireless" in their product types list.
Thirdly, we start creating the SSID for each network. Notice the `loop` and `loop_control` parameters. The task will be repeated with a different network ID (`item.id`).