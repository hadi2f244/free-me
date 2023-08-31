# Ansible Collection - hadi2f244.free_me

Ansible collection containing proxy and vpn clients

# Motivation

# Components

# Local Usage
It is recommended to install the collection by **ansible-galaxy collection** command, But there are some situtations where you need to edit the role by yourself manually. For ####


> Note: I realy appreciate contributions. For example adding new protocols and also improving current roles such as adding new protocols to v2ray/singbox role templates.

# Quick Start

I also provide simple Ansible playbooks to use diffrent free-me role in [free-me-test](https://github.com/hadi2f244/free-me-test) project.
# Contribution
Feel free to contribute your contribution to this project. It is simple and I really appreciate any help. Create an Issue for any question, suggestion or problem.

# Todo List
+ Add completely manual flag for vpn configs: openvpn role
+ V2ray: Vless + Vmess
+ Roles dependencies and documentation
+ L2TP
+ PPTP
+ Wireguard
+ SSH Tunnel
+ Blog posts (introduction + tutorial each configuration)
+ Connection test mechanisms
+ Add molecule + testinfra test for each role
+ Test collection on famous ansible projects such as Kubespray to make sure it works properly



# Refrence
[Make file usage for collection](https://github.com/andreygubarev/ansible-proxy/blob/main/Makefile)