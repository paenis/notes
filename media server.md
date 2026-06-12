## the problem
QNAP TS-251 died due to (probably) LPC clock bug (Celeron J1900)
won't boot at all; only way to repair is to solder a 100ohm resistor across CLK and GND

don't want to buy a new one :)
## try recovery
(qnap lvm data recovery bullshit)
https://github.com/mkke/qnap-recovery
## give up
[Perfect Media Server](https://perfectmediaserver.com)
install proxmox VE - https://xxx.local:8006/

postinstall:
- `bash -c "$(wget -qLO - https://github.com/community-scripts/ProxmoxVE/raw/main/tools/pve/post-pve-install.sh)"`
- `curl -fsSL https://tailscale.com/install.sh | sh`; `tailscale up`
	- easy remote access from https://pve.xxx.ts.net:8006
	- configure automatic boot on schedule and after power loss in BIOS

wipe disks and restore from 2023 backup