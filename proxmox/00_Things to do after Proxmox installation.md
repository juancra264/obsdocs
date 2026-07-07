# Thing to do after installing proxmox

## Update the system OS 
```bash
apt update 
apt dist-upgrade
apt autoremove
```

## Run the post install help script using GUI Shell

```bash
bash -c "$(curl -fsSL https://raw.githubusercontent.com/community-scripts/ProxmoxVE/main/tools/pve/post-pve-install.sh)"
```

## Install the SSL certificate for Web GUI.
For Custome Certificate:
PVE node -> System -> Certificates and then Upload Cert.

For Let's Encrypt check online the instructions.

## Install disks addional storage or disk as ZFS discs or RAIDs.
PVE node -> Disks -> ZFS then create as needed.

Configure ZFS ARC Limits (If using ZFS):
By default, ZFS can consume up to 50% of your system RAM for its read cache (ARC). If you have a low-RAM or medium-RAM system, limit this so your VMs don't run out of memory. 

Edit 
```bash
vim /etc/modprobe.d/zfs.conf
```

and add (for example, to limit ARC to 8GB):
```bash
options zfs zfs_arc_max=8589934592
```


##  Create a Admin user for OS and PVE webapp

As root, create user, assign password
```bash
apt install sudo
useradd -s /bin/bash -G sudo {user_name}
passwd {user_name}
```

Create User in PVE GUI
Datecenter -> Permissions -> User, Then create a PAM user.

Create Admins Group in PVE GUI 
Datecenter -> Permissions -> Groups

Create Permission for that Group
Datecenter -> Permissions
	Path / and role Administrator

Assign MFA (two Factor Authenticator) (for admin and root)
Datecenter -> Permissions -> Two Factor 

## Disable SSH Password Auth

Switch your CLI administration over to SSH keys. 
```bash
/etc/ssh/sshd_config 
```
ensure 
```bash
PasswordAuthentication no
```
is set, and restart the SSH service.




























### Switch Repository to Non-Production Version

```
nano /etc/apt/sources.list
```

Add the following lines to the bottom of the file:

```
# NOT recommended for production use
deb http://download.proxmox.com/debian/pve bookworm pve-no-subscription
# Not for production ceph
deb http://download.proxmox.com/debian/ceph-quincy bookworm no-subscription
```

### Disable the Production Repository

Next, disable the production repository by commenting out these lines in pve-enterprise.list:

```
nano /etc/apt/sources.list.d/pve-enterprise.list
```

Comment out this line:
```
#deb https://enterprise.proxmox.com/debian/pve bookworm pve-enterprise
```

Similarly, disable the enterprise repository for Ceph by commenting out these lines in ceph.list:

```
nano /etc/apt/sources.list.d/ceph.list
```

### VLAN Configuration

- Select your server.
- Go to “Network” in the menu.
- Select the Linux bridge (vmbpro#).
- Click “Edit” at the top of the window.
- Check the box that says “VLAN aware.”
- Press “OK.”

### Disable Subscription Popup
To remove the subscription popup, run the following command:

```
sed -Ezi.bak "s/(Ext.Msg.show\(\{\s+title: gettext\('No valid sub)/void\(\{ \/\/\1/g" /usr/share/javascript/proxmox-widget-toolkit/proxmoxlib.js && systemctl restart pveproxy.service
```
Afterward, reboot your server, log out of the Proxmox web GUI, clear your browser cache, and then log back in.

### Configure DNS and Install SSL Certificate.
- Configure DNS hostname like 

```
pve1.domain.local
```

- Upload the certificates or ACME module activation for your domain.

### Setup SMART monitoring for disks

```bash
smartctl -a /dev/sda
```


