## the problem
QNAP TS-251 died due to (probably) LPC clock bug (Celeron J1900)
won't boot at all; only way to repair is to solder a 100ohm resistor across CLK and GND

don't want to buy a new one :) everything is $200+ and fairly low specs. luckily, the drives are still functional

look for a used machine on ebay:
- HP elitedesk SFF mentioned often; tower isn't much bigger and has better drive options
	- go for around $120 + shipping, boot drive included
	- no hotswap drive bays :(
- future: rackmount server :P
	- surprisingly cheap!
	- probably very loud
	- might be hard to find replacement hardware
## try recovery
(qnap lvm data recovery bullshit)
https://github.com/mkke/qnap-recovery

they use normal md RAID arrays, but with some custom LVM thin pool setup
some people have managed to boot a modified version of the NAS firmware with QEMU and mount the drives that way, but i kept having issues

brute-force/forensic recovery (e.g. binwalk) didn't yield anything either
## give up
[Perfect Media Server](https://perfectmediaserver.com)
install proxmox VE - https://xxx.local:8006/

postinstall:
- remove no-subscription nags and enterprise apt repo + some cluster stuff: `bash -c "$(wget -qLO - https://github.com/community-scripts/ProxmoxVE/raw/main/tools/pve/post-pve-install.sh)"`
- set up tailscale: `curl -fsSL https://tailscale.com/install.sh | sh`; `tailscale up`
	- easy remote access from https://pve.xxx.ts.net:8006
		- alternatively, set up cf tunnel behind custom domain(???)
	- configure automatic boot on schedule and after power loss in BIOS
	- a KVM/IPMI setup would be nice but i don't have that, this is my replacement 
- install MergerFS: `curl -fsSL https://perfectmediaserver.com/scripts/install_mergerfs.sh | sh`
	- official debian repos lag behind
	- don't automate (yet) in case it breaks something during an update
- `apt install`
	- inxi
	- parted for `partprobe`
- partition disks: `sgdisk --clear --new=1:0:0 --typecode=1:8300 --change-name=1:data /dev/sd{b,c}` (as 2 commands) and `mkfs.xfs` on both
- 

wipe disks and restore from 2023 backup