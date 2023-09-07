# Shecan

+ To use **Shecan**, follow same steps as described in [free-me-test](https://github.com/hadi2f244/free-me-test/tree/main) project.
+ Instead change `inventory/mine/group_vars/all/dns_proxy.yml`, and run `playbooks/dns_proxy/on.yml`.
+ You can also stop and clean up the container configurations by `playbooks/dns_proxy/off.yml`.

## Custom code
Start and Stop the role in your Ansible playbooks:

```
- name: dns_proxy connect
  include_role:
    name: "hadi2f244.free_me.dns_proxy"
  vars:
    connected: true
    dnsproxy_dns_1: "{{ freeme_dns_proxy.dnsproxy_dns_1 }}"
    dnsproxy_dns_2: "{{ freeme_dns_proxy.dnsproxy_dns_2 }}"

<YOUR ANSIBLE CODE>

- name: dns_proxy disconnect
  include_role:
  name: "hadi2f244.free_me.dns_proxy"
  vars:
    connected: false
    dnsproxy_dns_1: "{{ freeme_dns_proxy.dnsproxy_dns_1 }}"
    dnsproxy_dns_2: "{{ freeme_dns_proxy.dnsproxy_dns_2 }}"
```