# Using Ansible with Cisco Meraki

![Meraki-Ansible](images/Meraki+Ansible.png)

[Ansible](https://ansible.com/) is an open-source software provisioning, configuration management, and application-deployment tool enabling Infrastructure as Code. For more information, refer [wikipedia](https://en.wikipedia.org/wiki/Ansible_(software)). Ansible is written in Python and can talk to managed nodes using SSH or HTTPS with REST for broad platform support and compatibility. This means Ansible supports a wide range of vendors, device types, and actions, so you can manage your workstations, servers, applications, network devices - and now [Cisco Meraki](https://meraki.cisco.com/) - with a single automation tool.

> 💡 Geeks will be happy to know the term [_ansible_](https://en.wikipedia.org/wiki/Ansible) originated in [a sci-fi novel](https://en.wikipedia.org/wiki/Rocannon%27s_World) as a contraction of "answerable" for a device allow its users to receive answers to their messages in a reasonable amount of time, even over interstellar distances.

One of the greatest features of Ansible is that it is **agentless**. You do not need to install anything on the managed node to control. Linux workstations and servers can be controlled over SSH and Cisco Meraki is controlled using REST APIs. Other protocols are possible using many different Python libraries.

Another feature of Ansible is that when configurations are run by modules, they set things to a desired state. Additional runs of the same configuration results in no changes. This is called **_idempotence_**, from the Latin: idem + potence (same + power). In mathematics and computer science, it is “the property of certain operations that can be applied multiple times without changing the result beyond the initial application”. This means running an Ansible playbook results in a consistent configuration state whether your managed node needed no changes, a little, or a lot.

> 💡 idempotence: The property of certain operations that can be applied multiple times without changing the result beyond the initial application.

![Ansible-Idempotence](images/Ansible-Idempotence.png)