# Todo List

+ Cleanup configs:

    + Remove systemd service in V2ray and Singbox in disconnect mode.

+ Add SSH Tunnel
+ Add `SOCKS_PROXY`
+ Resolve the issue related to remaining `HTTP_PROXY` and `HTTPS_PROXY` variable after runnging `off.yml` on localhost
+ Check v2ray/singbox services status after starting (Assert if there is an issue on service restarting)
+ Add Socks to *env_proxy*, *container_proxy*, *apt_proxy*, *singbox*, and *v2ray*
+ Add link based V2ray/Singbox configurations.
+ Tshoot OVPN, and Add a completely manual flag for VPN configs: OVPN role
+ L2TP
+ PPTP
+ V2ray: Vless + Vmess
+ Roles dependencies and documentation
+ Wireguard
+ Blog posts (introduction + tutorial each configuration)
+ Connection test mechanisms
+ Add molecule + test-infra test for each role