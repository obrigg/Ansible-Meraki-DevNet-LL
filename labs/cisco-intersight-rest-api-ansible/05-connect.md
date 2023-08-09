## Configure Meraki Dashboard API Settings

Now that you installed the Meraki Ansible Collection, you can use it to configure Meraki's Dashboard API settings. First you need API key credentials from your Meraki account. If you don't have an account, you can use Cisco [DevNet Sandbox](https://developer.cisco.com/site/sandbox/).

### API Keys

To generate an Meraki API Key, use [the following guide](https://documentation.meraki.com/General_Administration/Other_Topics/Cisco_Meraki_Dashboard_API).

Meraki's Ansible Collection can use environment variables for API Key.  Key data can also be set in playbooks, inventory files, or other variable sources from Ansible. In this lab the example playbooks will lookup data from environment variables.

> It is not recommended to save sensitive information (e.g. credentials and API keys) in an unencrypted file that can accidentally be uploaded with the code to a public repository.

The commands below set the environment variables used by Ansible with data from the files created above.

```bash
export MERAKI_DASHBOARD_API_KEY= <your API key>
```

### Validating the settings

To validate the environment variable is set and the API key is valid, you can run the following playbook, save it as `who_am_i.yml`

```
---
- hosts: meraki_servers
  gather_facts: false
  tasks:
    - name: Get my administered identities
      cisco.meraki.administered_identities_me_info:
      register: result

    - name: Show result
      ansible.builtin.debug:
        msg: "{{ result }}"
```
and run it using the command: `ansible-playbook -i hosts who_am_i.yml`

<details><summary>Click here to see the expected output</summary>
<pre><code>
PLAY [meraki_servers] ***************************************************************************************************************************************************************************************

TASK [Get my administered identities] ***********************************************************************************************************************************************************************
ok: [meraki_server]

TASK [Show result] ******************************************************************************************************************************************************************************************
ok: [meraki_server] => {
    "msg": {
        "changed": false,
        "failed": false,
        "meraki_response": {
            "authentication": {
                "api": {
                    "key": {
                        "created": true
                    }
                },
                "mode": "email",
                "saml": {
                    "enabled": false
                },
                "twoFactor": {
                    "enabled": false
                }
            },
            "email": "devnetmerakiadmin@cisco.com",
            "lastUsedDashboardAt": "2023-01-31T16:18:46.000000Z",
            "name": "DevNet Meraki Admin"
        },
        "result": ""
    }
}

PLAY RECAP **************************************************************************************************************************************************************************************************
meraki_server              : ok=2    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0</code></pre>
</details> 
