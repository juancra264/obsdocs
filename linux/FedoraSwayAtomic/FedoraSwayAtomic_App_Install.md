# Installing Apps 

## Installing vim or neovim

1 Package Layering (Native Install): 

Use rpm-ostree to layer packages onto the immutable base. This requires a reboot to take effect.

```bash
sudo rpm-ostree install vim-enhanced
# or for Neovim
sudo rpm-ostree install neovim
```

Note: You must reboot the system after running this command for the new layer to be applied. 

2 Toolbox (Recommended for Development): 

Use Fedora Toolbox to create a mutable container environment. This is preferred for development tools as it avoids reboots and keeps the base system clean.

```bash
toolbox create
toolbox enter
sudo dnf install vim-enhanced
```

Note: Inside the toolbox container, you can use standard dnf commands. Your home directory files are shared with the host, so your configs will persist.

## Installing ZSH

To install Zsh on Fedora Sway Atomic, you must first install the base package and the utility required to change your default shell, as the system is immutable.

1. Install Required Packages
Open your terminal and run the following command to install Zsh, Git (for Oh My Zsh), and util-linux-user (which provides the chsh command):

```bash
sudo dnf install zsh curl git util-linux-user
```

2. Set Zsh as Default Shell
Use the chsh command to switch your default shell from Bash to Zsh:

```bash
chsh -s /usr/bin/zsh
```

3. Restart Terminal
Close all terminal windows and open a new one. Zsh will launch and typically present an initial configuration wizard for new users. 

Note on Fedora Sway Atomic:
Because Fedora Sway Atomic uses an immutable root filesystem (via rpm-ostree), standard dnf install commands may not persist across reboots in all configurations. If you encounter issues, you may need to use package layering (via rpm-ostree install zsh) or install Zsh within a Toolbx container, which is the recommended environment for development tools on Atomic systems.

