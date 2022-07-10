# System Setup for macOS

Run all of these steps in sequence when setting up a new macOS system. This is tested on macOS 12.4 (Monterey) and may not work on earlier or later releases.

## Install all OS Updates

### Install Rosetta 2

```
/usr/sbin/softwareupdate --install-rosetta --agree-to-license
```

## Homebrew

```
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

brew tap hashicorp/tap

brew install gpg htop nmap wget jq httpie mas bat dog exa

brew install --cask docker homebrew/cask-versions/google-chrome-beta docker maestral little-snitch 1password 1password-cli spotify iterm2 aerial visual-studio-code github homebrew/cask-versions/slack-beta istat-menus soundsource transmit

brew install hashicorp/tap/packer hashicorp/tap/terraform
```

### Only installed on personal systems

```
brew install --cask battle-net discord steam
```

## Mac App Store

You'll need to manually launch the Mac App Store and sign in with your Apple ID before any of the next commands will work.

```
# XCode, NextDNS, Amphetamine, WireGuard
mas install 497799835 1464122853 937984704 1451685025

# Bear, Brother Scanner Software, Day One, LINE, Keynote, Soulver, Pixelmator
mas install 1091189122 1193539993 1055511498 539883307 409183694 1508732804 407963104
```

## Other Apps

These applications aren't in either Homebrew or the Mac App Store and have to be manually installed.

### Tailscale

```
cd /tmp && \
wget https://pkgs.tailscale.com/stable/Tailscale-1.26.2-macos.zip && \
unzip Tailscale-1.26.2-macos.zip && \
mv Tailscale.app /Applications/ && \
```

### Stream Deck

```
cd /tmp && \
wget https://edge.elgato.com/egc/macos/sd/Stream_Deck_5.3.1.15197.pkg && \
open Stream_Deck_5.3.1.15197.pkg && \
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