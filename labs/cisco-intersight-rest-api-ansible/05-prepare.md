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