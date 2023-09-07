# Kubespray

One of the biggest Ansible project is Kubespray. One of the issue you may seem first is filtering or similar obstacles to install requirements like container and packages.

Add *start* and *stop* Proxy/VPN block at the begging of `cluster.yml` or `playbooks/cluster.yml`:
For example:

# V2ray

+ Add a variable `use_freeme: true` to `inventory/mycluster/group_vars/all/all.yml` to enable/disable using Freeme.
+ Add v2ray configuration to `all.yml`. Example:
```
freeme_v2ray:
  # v2ray_version: "5.7.0"
  set_env_proxy: false
  set_apt_proxy: true
  set_container_proxy: true

  v2ray_addr:
  v2ray_port:
  v2ray_uuid:
  v2ray_trojan_password:
  proxy_socks_port: 10808
  proxy_http_port: 10809

  backup_previous_config: false

  use_custom_config: false # Note: Change proxy_socks_port/proxy_http_port accordingly if you use custom config
  custom_config: |
    {
      "inbounds": [
        ...
      ],
      "outbounds": [
        ...
      ],
      "routing": {
        ...
      }
    }
```
> This config is same as [free-me-test](https://github.com/hadi2f244/free-me-test/blob/main/inventory/sample/group_vars/all/v2ray.yml) v2ray configs.
> Important: Make sure you set `set_env_proxy: false` in the above config to avoid conflict with kubespray configs.

+ Also, make sure you change this part as well:
```
## Set these proxy values in order to update package manager and docker daemon to use proxies
http_proxy: "http://127.0.0.1:{{freeme_v2ray.proxy_http_port}}"
https_proxy: "http://127.0.0.1:{{freeme_v2ray.proxy_http_port}}"
```

+ Create `playbooks/proxy_on.yml` and `playbooks/proxy_off.yml`

> These file are same as [v2ray start](https://github.com/hadi2f244/free-me-test/blob/main/playbooks/v2ray/on.yml) and [v2ray stop](https://github.com/hadi2f244/free-me-test/blob/main/playbooks/v2ray/on.yml) in free-me-test project.

**proxy_on.yml**:
```
- hosts: all
  gather_facts: True
  tasks:
    - name: v2ray connect
      include_role:
        name: "hadi2f244.free_me.v2ray"
      vars:
        connected: true
        # v2ray_version: "{{ freeme_v2ray.v2ray_version }}"
        set_env_proxy: "{{ freeme_v2ray.set_env_proxy }}"
        set_apt_proxy: "{{ freeme_v2ray.set_apt_proxy }}"
        set_container_proxy: "{{ freeme_v2ray.set_container_proxy }}"
        v2ray_addr: "{{ freeme_v2ray.v2ray_addr }}"
        v2ray_port: "{{ freeme_v2ray.v2ray_port }}"
        v2ray_uuid: "{{ freeme_v2ray.v2ray_uuid }}"
        proxy_socks_port: "{{ freeme_v2ray.proxy_socks_port }}"
        proxy_http_port: "{{ freeme_v2ray.proxy_http_port }}"
        v2ray_trojan_password: "{{ freeme_v2ray.v2ray_trojan_password }}"
        backup_previous_config: "{{ freeme_v2ray.backup_previous_config }}"
        use_custom_config: "{{ freeme_v2ray.use_custom_config }}"
        custom_config: "{{ freeme_v2ray.custom_config }}"
```

**proxy_off.yml**:
```

- hosts: all
  gather_facts: True
  tasks:
    - name: v2ray disconnect
      include_role:
        name: "hadi2f244.free_me.v2ray"
      vars:
        connected: false
        # v2ray_version: "{{ freeme_v2ray.v2ray_version }}"
        set_env_proxy: "{{ freeme_v2ray.set_env_proxy }}"
        set_apt_proxy: "{{ freeme_v2ray.set_apt_proxy }}"
        set_container_proxy: "{{ freeme_v2ray.set_container_proxy }}"
        v2ray_addr: "{{ freeme_v2ray.v2ray_addr }}"
        v2ray_port: "{{ freeme_v2ray.v2ray_port }}"
        v2ray_uuid: "{{ freeme_v2ray.v2ray_uuid }}"
        proxy_socks_port: "{{ freeme_v2ray.proxy_socks_port }}"
        proxy_http_port: "{{ freeme_v2ray.proxy_http_port }}"
        v2ray_trojan_password: "{{ freeme_v2ray.v2ray_trojan_password }}"
        backup_previous_config: "{{ freeme_v2ray.backup_previous_config }}"
        use_custom_config: "{{ freeme_v2ray.use_custom_config }}"
        custom_config: "{{ freeme_v2ray.custom_config }}"
```

+ Edit `cluster.yml` or `playbooks/cluster.yml` like below:

```

...

- name: Gather facts
  tags: always
  import_playbook: facts.yml

- name: Proxy on
  tags: always
  import_playbook: proxy_on.yml

...


- name: Proxy off
  tags: always
  import_playbook: proxy_off.yml

```

# 2. Other options Singbox


Steps are like above. Use these files instead
## Singbox:
+ [Configs](https://github.com/hadi2f244/free-me-test/blob/main/inventory/sample/group_vars/all/singbox.yml)
+ [proxy_on](https://github.com/hadi2f244/free-me-test/tree/main/playbooks/singbox/on.yml)
+ [proxy_off](https://github.com/hadi2f244/free-me-test/tree/main/playbooks/singbox/off.yml)

## Shecan
+ [Configs](https://github.com/hadi2f244/free-me-test/blob/main/inventory/sample/group_vars/all/dns_proxy.yml)
+ [proxy_on](https://github.com/hadi2f244/free-me-test/tree/main/playbooks/dns_proxy/on.yml)
+ [proxy_off](https://github.com/hadi2f244/free-me-test/tree/main/playbooks/dns_proxy/off.yml)

## HTTP Proxy
You should call `env_proxy` to set HTTP/HTTPS env variable to install packages and `container_proxy` to make continer runtime use the proxy.
Configs:
+ [env_proxy Configs](https://github.com/hadi2f244/free-me-test/blob/main/inventory/sample/group_vars/all/dns_proxy.yml)
+ [container_runtime Configs](https://github.com/hadi2f244/free-me-test/blob/main/inventory/sample/group_vars/all/container_proxy.yml)

For `proxy_on.yml`, combine these playbooks:
+ [env_proxy proxy_on](https://github.com/hadi2f244/free-me-test/tree/main/playbooks/dns_proxy/on.yml)
+ [container_runtime proxy_on](https://github.com/hadi2f244/free-me-test/tree/main/playbooks/container_proxy/on.yml)

For `proxy_off.yml`, combine these playbooks:
+ [env_proxy proxy_off](https://github.com/hadi2f244/free-me-test/tree/main/playbooks/dns_proxy/off.yml)
+ [container_runtime proxy_off](https://github.com/hadi2f244/free-me-test/tree/main/playbooks/dns_proxy/off.yml)