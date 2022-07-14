# System Setup for macOS

Run all of these steps in sequence when setting up a new macOS system. This is tested on macOS 12.4 (Monterey) and may not work on earlier or later releases.

## Basic OS Config

### Fully update OS

```
/usr/sbin/softwareupdate -ia
```

### Install Rosetta 2

```
/usr/sbin/softwareupdate --install-rosetta --agree-to-license
```

### Enable the OS Firewall

```
sudo defaults write /Library/Preferences/com.apple.alf globalstate -int 1
```

### Enable FileVault

```
/usr/bin/fdesetup enable
```

## Homebrew

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

### Auth with Mac App Store

This must be done manually. Open the Mac App Store and authenticate with your Apple ID before the next steps.

```
open /System/Applications/App\ Store.app
```

### Install Homebrew/MAS software

This first command is to be used on any system (personal or work)

```
curl -fsSL https://raw.githubusercontent.com/tomcook/system-setup/main/macos/Brewfile | brew bundle --file=-
```

This command is just for use on personal systems

```
curl -fsSL https://raw.githubusercontent.com/tomcook/system-setup/main/macos/Brewfile-personal | brew bundle --file=-
```

## Other Apps

These applications aren't in either Homebrew or the Mac App Store and have to be manually installed.

### Tailscale

```
cd /tmp && \
wget https://pkgs.tailscale.com/stable/Tailscale-1.26.2-macos.zip && \
unzip Tailscale-1.26.2-macos.zip && \
mv Tailscale.app /Applications/
```

### Stream Deck

```
cd /tmp && \
wget https://edge.elgato.com/egc/macos/sd/Stream_Deck_5.3.1.15197.pkg && \
open Stream_Deck_5.3.1.15197.pkg
```

### Reflex

```
cd ~/Downloads && \
wget http://stuntsoftware.com/download/reflex_1.2.zip
```

## App Follow-up

- Little Snitch should be setup first. It'll require a number of permissions that have to be granted manually.
- Tailscale will need to be signed-in, allowed to function as a VPN, and set up manually.
- Soundsource will need a full manual configuration and possibly a reboot
- NextDNS needs to be started and configured with the correct Configuration ID


## Finder / UI Customizations

### Remove everything from the Dock

```
defaults write com.apple.dock persistent-apps -array && killall Dock
```

### Set hot corners

Instructions on what all of this means can be found [here](https://blog.jiayu.co/2018/12/quickly-configuring-hot-corners-on-macos/).

```
defaults write com.apple.dock wvous-bl-corner -int 5 && \
defaults write com.apple.dock wvous-bl-modifier -int 0 && \
defaults write com.apple.dock wvous-br-corner -int 4 && \
defaults write com.apple.dock wvous-br-modifier -int 0 && \
defaults write com.apple.dock wvous-tl-corner -int 2 && \
defaults write com.apple.dock wvous-tl-modifier -int 0 && \
killall Dock
```

## dotfiles

## Misc

### Change to the bash shell

```
chsh -s /bin/bash
```

### iStat Menu Config