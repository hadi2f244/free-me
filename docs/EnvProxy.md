# Environment Proxies
During installing packages or even a simple command like *curl* you may need to tunnel the traffic through a proxy.
After a complete investigation of the related solutions, I find it to split this goal through two roles:

+ `env_proxy`: This rule changes `/etc/environment` file and adds some env variables like *HTTP_PROXY*. Note: Make sure you restart all shells to load new env variables after you apply this role.
+ `apt_proxy`: You may just need *apt* command to use a proxy.

# Example
+ Clone [free-me-test](https://github.com/hadi2f244/free-me-test) project.
+ Follow Quick Start steps. Change `inventory/mine/group_vars/all/env_proxy.yml`, and run `playbooks/env_proxy/on.yml`.
+ You can also stop and clean up the container configurations by `playbooks/env_proxy/off.yml`.

## Custom code
Start and Stop the role in your Ansible playbooks:


```
- name: env_proxy connect
  include_role:
    name: "hadi2f244.free_me.env_proxy"
  vars:
    connected: true
    http_proxy: "{{ freeme_env_proxy.http_proxy }}"
    https_proxy: "{{ freeme_env_proxy.https_proxy }}"

<YOUR ANSIBLE CODE>

- name: env_proxy disconnect
  include_role:
  name: "hadi2f244.free_me.env_proxy"
  vars:
    connected: false
    http_proxy: "{{ freeme_env_proxy.http_proxy }}"
    https_proxy: "{{ freeme_env_proxy.https_proxy }}"
```

I have tried to simplify all proxy connector rules by the same template. So, you can use `apt_proxy` and `container_proxy` similarly. Check `on.yml` and `off.yml` in [free-me-test](https://github.com/hadi2f244/free-me-test).