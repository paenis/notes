## try recovery
(qnap lvm data recovery bullshit)
https://github.com/mkke/qnap-recovery
## give up


https://10.10.11.26:8006/

postinstall:
- `bash -c "$(wget -qLO - https://github.com/community-scripts/ProxmoxVE/raw/main/tools/pve/post-pve-install.sh)"`
- `curl -fsSL https://tailscale.com/install.sh | sh`; `tailscale up`
	- https://pve.xxx.ts.net:8006