## Ansible and Meraki Collection Installation

The Learning Labs environment is Linux based, and you will now install Ansible using Python's pip utility.

Install Ansible
```bash
sudo pip install ansible
```
<details><summary>Click here to see output</summary>
<pre><code>
Collecting ansible
  Downloading ansible-7.4.0-py3-none-any.whl (43.3 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 43.3/43.3 MB 2.2 MB/s eta 0:00:00
Collecting ansible-core~=2.14.4
  Downloading ansible_core-2.14.4-py3-none-any.whl (2.2 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 2.2/2.2 MB 2.3 MB/s eta 0:00:00
...
Successfully installed MarkupSafe-2.1.2 ansible-7.4.0 ansible-core-2.14.4 jinja2-3.1.2 resolvelib-0.8.1
</code></pre>
</details>

You can now check the Ansible version and Python in use.

```bash
ansible --version
```
<details><summary>Click here to see output</summary>
<pre><code>
ansible [core 2.14.4]
  config file = None
  configured module search path = ['/home/developer/.ansible/plugins/modules', '/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/local/lib/python3.10/site-packages/ansible
  ansible collection location = /home/developer/.ansible/collections:/usr/share/ansible/collections
  executable location = /usr/local/bin/ansible
  python version = 3.10.5 (main, Jun 24 2022, 02:43:59) [GCC 10.2.1 20210110] (/usr/local/bin/python)
  jinja version = 3.1.2
  libyaml = False</code></pre>
</details>

## Intersight Collection Installation

Cisco Meraki's Ansible Collection is available from [Ansible Galaxy](https://galaxy.ansible.com/cisco/meraki).

There is an installation command line that can by copy/pasted from Galaxy:

> **Note:** --force can be added to overwrite any existing Meraki Collection installations.

```bash
ansible-galaxy collection install cisco.meraki
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
