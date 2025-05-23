# System Setup for macOS

Run all of these steps in sequence when setting up a new macOS system. This is tested on macOS 12.4 (Monterey) and may not work on earlier or later releases.

## Basic OS Config

### Fully update OS

```
/usr/sbin/softwareupdate -ia
```

### Preferences for automatic updates

```
osascript -e "tell application \"System Preferences\" to quit" && \
sudo softwareupdate --schedule off && \
sudo defaults write /Library/Preferences/com.apple.SoftwareUpdate.plist AutomaticCheckEnabled -bool YES && \
sudo defaults write /Library/Preferences/com.apple.SoftwareUpdate.plist AutomaticDownload -bool YES && \
sudo defaults write /Library/Preferences/com.apple.SoftwareUpdate.plist ConfigDataInstall -bool YES && \
sudo defaults write /Library/Preferences/com.apple.SoftwareUpdate.plist CriticalUpdateInstall -bool YES && \
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

Download and install the .pkg from https://pkgs.tailscale.com/stable/#macos

## App Follow-up

- Little Snitch should be setup first. It'll require a number of permissions that have to be granted manually.
- Tailscale will need to be signed-in, allowed to function as a VPN, and set up manually.
- Soundsource will need a full manual configuration and possibly a reboot

## Finder / UI Customizations

### Dock customization

- Remove all icons from the Dock
- Make the Dock appear instantly instead of slowly appearing
- Very small, immutable size Dock icons
- Only show running apps
- Use the 'scale' animation to minimize windows to the Dock

```
defaults write com.apple.dock persistent-apps -array && \
defaults write com.apple.dock autohide-delay -float 0.5 && \
defaults write com.apple.dock autohide-time-modifier -int 0.5 && \
defaults write com.apple.dock tilesize -int 12 && \
defaults write com.apple.dock size-immutable -bool yes && \
defaults write com.apple.dock static-only -bool true && \
defaults write com.apple.dock mineffect -string scale && \
killall Dock
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

### No drop shadow behind screenshots

```
defaults write com.apple.screencapture disable-shadow -bool true && \
killall SystemUIServer
```

## dotfiles

## shell

Set fish as an allowed shell

```
echo /opt/homebrew/bin/fish | sudo tee -a /etc/shells
```

Change shell to fish

```
chsh -s /opt/homebrew/bin/fish
```

## Misc

### iStat Menu Config
