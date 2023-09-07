# Container Runtime Proxy
To make container runtime use proxy use `container_proxy` role. It supports Docker, ContainerD, and CRIO.
First, it checks which runtime is installed, then proper configurations will be applied.

# Example
+ Clone [free-me-test](https://github.com/hadi2f244/free-me-test) project.
+ Follow Quick Start steps. Change `inventory/mine/group_vars/all/container_proxy.yml`, and run `playbooks/container_proxy/on.yml`.
+ You can also stop and clean up the container configurations by `playbooks/container_proxy/off.yml`.
+ You can Start and Stop the role in your Ansible playbooks:

```
- name: container_proxy connect
  include_role:
    name: "hadi2f244.free_me.container_proxy"
  vars:
    connected: true
    http_proxy: "{{ freeme_container_proxy.http_proxy }}"
    https_proxy: "{{ freeme_container_proxy.https_proxy }}"

<YOUR ANSIBLE CODE>

- name: container_proxy disconnect
  include_role:
  name: "hadi2f244.free_me.container_proxy"
  vars:
    connected: false
    http_proxy: "{{ freeme_container_proxy.http_proxy }}"
    https_proxy: "{{ freeme_container_proxy.https_proxy }}"
```