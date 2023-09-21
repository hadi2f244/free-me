# Notes

+ If you set env proxies`(set_env_proxy=true)` on the target host, make sure you start again to use updated env variables


# Notes:
    ALL_PROXY=socks5h://localhost:65432 curl -vi 10.0.0.107:80/dashboard

+ **[ansible host]**: the host where ansible playbook runs
+ **[target server]**: the ansible target
+ **[tunnel server]**: the server that we wants to create tunnel on to send traffic to.


# Todo:
+ conert socks to http (https://superuser.com/questions/280129/http-proxy-over-ssh-not-socks) or **corkscrew** command
+ custom ssh options like ssh_port
+ transfer ssh key between **[ansible host]** and **[target server]**
+ security issue with transfering ssh key to remote host
+ ability to create temporary ssh key on **[tunnel server]** + a ability to as a systemd service on **[tunnel server]** to delete the key on target server
+ Is it possible to use ssh in Ansible for this purpose?
+ Connection types:
    + **[ansible host]** can connect to **[tunnel server]**
    + just **[target server]** can connect to **[tunnel server]**
+ cleanup keys after connection disconnected
+ Limit ssh client to just create tunnel not to run command on target server
+ Print a prompt that notice the user that leaving created temporary ssh tunnel should be removed with disconnect roles.
