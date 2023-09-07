## Local Usage
You may need to use the roles to connect local env to a proxy or VPN.

Follow the steps same as the [free-me-test](https://github.com/hadi2f244/free-me-test) project. Just add this line to inventory;
`localhost ansible_user=root ansible_host=127.0.0.1`

Use these commands to start and stop:
```
ansible-playbook --vault-password-file ./.vault  -i inventory/mine/inventory.ini  --connection=local  playbooks/v2ray/on.yml -b -l "localhost"

ansible-playbook --vault-password-file ./.vault  -i inventory/mine/inventory.ini  --connection=local  playbooks/v2ray/off.yml -b -l "localhost"
```