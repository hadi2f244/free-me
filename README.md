# Ansible Collection - hadi2f244.free_me

A versatile Ansible collection for proxy and VPN clients.

# Motivation

I created this *Ansible collection* with a deep motivation to empower DevOps, SRE, and sysadmins in regions facing filtering and sanctions, such as Iran. My goal is to help them overcome the obstacles they encounter when trying to install essential tools like *Docker* and *Kubernetes*. I provided practical solutions within Ansible playbooks, including addressing issues like installing Kubernetes with *Kubespray*, package installations, and downloading container images.

# Components/Roles
Every type of client is in a different role. Some of them are VPN/proxy clients and some are just a connection to a proxy.

"The main idea is to simplify all the solutions to work as `on` and `off` module. In Ansible it means all of starting/connecting and stopping/disconnecting steps are done in `on.yml` and `off.yml` respectively"

List of roles:

Proxy connectors:

+ `env_proxy`: In the situation where you started a Http/Https and want your shell to use it.
+ `apt_proxy`: Make APT to use HTTP/HTTPS proxy
+ `dns_proxy`: You may need to use some anti-filtering solution that is based on DNS like *Shecan*
+ `container_proxy`: Force Docker, Containerd, and CRIO services to use a proxy.

Clients:
+ `v2ray`: V2ray client that provides Socks/HTTP proxy and you can also use proxy connectors to use the proxy(It contains *env_proxy*, *apt_proxy*,and *container_proxy*)
+ `Singbox`: Like V2ray client
+ `OVPN`: OVPN VPN client.

> I am trying to implement other Proxy/VPN clients as well.

# Quick Start
> Important: I provided [free-me-test](https://github.com/hadi2f244/free-me-test) project you can clone it and Follow the instructions to test all roles.

## Installation Instructions
`ansible-galaxy collection install hadi2f244.free_me:<version>`

# Local Usage
It is recommended to install the collection by **ansible-galaxy collection** command, But there are some situations where you need to edit the role by yourself manually. Follow [Local test collection](https://github.com/hadi2f244/free-me-test#local-test-collection) section in free-me-test project.

# Use Cases
I have used this code during different Ansible projects (e.g. Kubespray), I would share my experiences in the [Documentation](https://github.com/hadi2f244/free-me/tree/main/docs) separately.

+ [Roles Details](https://github.com/hadi2f244/free-me/tree/main/docs/Roles.md)
+ [Environment Variable Proxy](https://github.com/hadi2f244/free-me/tree/main/docs/EnvProxy.md)
+ [Container Runtime Proxy](https://github.com/hadi2f244/free-me/tree/main/docs/ConatinerRuntimes.md)
+ [Shecan](https://github.com/hadi2f244/free-me/tree/main/docs/Shecan.md)
+ [Kubespray](https://github.com/hadi2f244/free-me/tree/main/docs/Kubespray.md)


# Contribution
If you've ever considered joining the tech party, here's your invite! Contribute your skills (code), and together, we'll make tech tasks a breeze. Your help is a game-changer! 🚀


> Important: Please create an Issue for any question, suggestion, or problem.

> Note: Feel free to contribute your contribution to this project. I really appreciate contributions. For example, adding new protocols and also improving current roles such as adding new protocols to v2ray/singbox role templates.

# Todo List
+ Remaining `HTTP_PROXY` and `HTTPS_PROXY` variable after runnging `off.yml` on localhost
+ Check v2ray/singbox services status after starting (Assert if there is an issue on service restarting)
+ Add Socks to *env_proxy*, *container_proxy*, *apt_proxy*, *singbox*, and *v2ray*
+ Add link based V2ray/Singbox configurations.
+ SSH Tunnel
+ Tshoot OVPN, and Add a completely manual flag for VPN configs: OVPN role
+ L2TP
+ PPTP
+ V2ray: Vless + Vmess
+ Roles dependencies and documentation
+ Wireguard
+ Blog posts (introduction + tutorial each configuration)
+ Connection test mechanisms
+ Add molecule + test-infra test for each role

# Refrence
[Make file usage for collection](https://github.com/andreygubarev/ansible-proxy/blob/main/Makefile)