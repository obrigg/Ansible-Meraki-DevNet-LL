## Ansible and Meraki Collection Installation

The Learning Labs environment is Linux based, and you will now install Ansible using Python's pip utility.

Install Ansible
```bash
pip install ansible
```
<details><summary>Click here to see output</summary>
<pre><code>
Collecting ansible
  Downloading ansible-8.2.0-py3-none-any.whl (45.1 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 45.1/45.1 MB 28.8 MB/s eta 0:00:00
Collecting ansible-core~=2.15.2
  Downloading ansible_core-2.15.3-py3-none-any.whl (2.2 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 2.2/2.2 MB 35.7 MB/s eta 0:00:00
...
Successfully installed MarkupSafe-2.1.3 ansible-8.2.0 ansible-core-2.15.3 jinja2-3.1.2 resolvelib-1.0.1
</code></pre>
</details>

You can now check the Ansible version and Python in use.

```bash
ansible --version
```
<details><summary>Click here to see output</summary>
<pre><code>
ansible [core 2.15.3]
  config file = None
  configured module search path = ['/home/developer/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
  ansible python module location = /home/developer/.local/lib/python3.10/site-packages/ansible
  ansible collection location = /home/developer/.ansible/collections:/usr/share/ansible/collections
  executable location = /home/developer/.local/bin/ansible
  python version = 3.10.4 (main, May 11 2022, 07:26:18) [GCC 10.2.1 20210110] (/usr/local/bin/python)
  jinja version = 3.1.2
  libyaml = False
</code></pre>
</details>

Install the Meraki Python SDK
```bash
pip install meraki
```
<details><summary>Click here to see output</summary>
<pre><code>
Defaulting to user installation because normal site-packages is not writeable
Collecting meraki
  Downloading meraki-1.36.0-py3-none-any.whl (255 kB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 255.2/255.2 kB 25.5 MB/s eta 0:00:00
...
Installing collected packages: multidict, frozenlist, charset-normalizer, async-timeout, yarl, aiosignal, aiohttp, meraki
Successfully installed aiohttp-3.8.5 aiosignal-1.3.1 async-timeout-4.0.3 charset-normalizer-3.2.0 frozenlist-1.4.0 meraki-1.36.0 multidict-6.0.4 yarl-1.9.2
</code></pre>
</details>

## Meraki Collection Installation

Cisco Meraki's Ansible Collection is available from [Ansible Galaxy](https://galaxy.ansible.com/cisco/meraki).

There is an installation command line that can by copy/pasted from Galaxy:

> **Note:** --force can be added to overwrite any existing Meraki Collection installations.

```bash
ansible-galaxy collection install git+https://github.com/meraki/dashboard-api-ansible.git -f
```
<details><summary>Click here to see output</summary>
<pre><code>
Starting galaxy collection install process
Process install dependency map
Starting collection install process
Downloading https://galaxy.ansible.com/download/cisco-meraki-1.0.25.tar.gz to /home/developer/.ansible/tmp/ansible-local-43t8lfr33w/tmpn7ganlal/cisco-meraki-1.0.25-rt79a452
Installing 'cisco.meraki:1.0.25' to '/home/developer/.ansible/collections/ansible_collections/cisco/meraki'
cisco.meraki:1.0.25 was installed successfully
</code></pre>
</details> 

## Configure Meraki Dashboard API Settings

Now that you installed the Meraki Ansible Collection, you can use it to configure Meraki's Dashboard API settings. First you need API key credentials from your Meraki account. If you don't have an account, you can use Cisco [DevNet Sandbox](https://developer.cisco.com/site/sandbox/).

### Meraki API Keys

To generate an Meraki API Key, use [the following guide](https://documentation.meraki.com/General_Administration/Other_Topics/Cisco_Meraki_Dashboard_API).

Meraki's Ansible Collection can use environment variables for API Key.  Key data can also be set in playbooks, inventory files, or other variable sources from Ansible. In this lab the example playbooks will lookup data from environment variables.

> It is not recommended to save sensitive information (e.g. credentials and API keys) in an unencrypted file that can accidentally be uploaded with the code to a public repository.

The commands below set the environment variables used by Ansible with data from the files created above.

```bash
export MERAKI_DASHBOARD_API_KEY=<your API key>
```