#  🐧 dotfiles-linux

## System Settings:
```
# Auto timezone
# System Settings > Time and Date > Set time and date automatically

# Breath2Dark Colors
# System Settings > Colors > Breath2Dark
# System Settings > Icons > Breath2 Dark
# System Settings > Startup and Shutdown > Breath2

# Setup Caps Lock map to Ctrl
# System Settings > Hardware > Input Devices > Keyboard > Advanced > Caps Lock behavior > Caps Lock is also a Ctrl

# Setup Left Alt to Ctrl
# System Settings > Hardware > Input Devices > Keyboard > Advanced > Ctrl position > Left Alt as Ctrl, Left Ctrl as Win, Left Win as Left Alt

# Drop Yakuake from startup
# System Settings > Startup and Shutdown > Yakuake
```

## Stylize with Nord (optional)
```
# System Settings > Global Theme > Get New Global Themes... > Search for "Nordic KDE" > Install > Select and Apply
# System Settings > Application Style > Configure GNOME/GTK Application Style... > Get New GNOME/GTK Application Styles... > Search for Nordic > Install > Nordic-darker.tar.xz > Close > Set "GTK theme:" to "Nordic-darker" > Apply
# System Settings > Colors > Nordic-Darker
# System Settings > Icons > Get New Icons... > Search for Nordic > Install, select, and apply
# System Settings > Startup and Shutdown > Logni Screen (SDDM) > Nordic

# Konsole > Settings > Manage Profiles... > New > Name BAM > Appearance > Get New... > Search for Nordic > Select, apply > Set as Default
```

## To Install:
```bash
# Open Konsole (top left quarter)
# Open Kate (top right quarter)
# Open Firefox (bottom left quarter)

# Install yay (https://github.com/Jguer/yay)
sudo pacman -S base-devel yay

# Perform system update
# System Settings > Kernel > Install latest and reboot to take affect

yay -Syu --devel --timeupdate

# Install needed packages
yay -S wget git gvim github-cli rcm

# Install oh-my-zsh
sh -c "$(wget https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions

echo $SHELL # Should return `/usr/bin/zsh`

# Log out of user and back in

# Install powerlevel10k
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/themes/powerlevel10k
p10k configure

# Install keybase and GPG keys
yay -S keybase-bin
run_keybase
keybase pgp list
keybase pgp export -q <ID_FROM_ABOVE> | gpg --import
keybase pgp export -q <ID_FROM_ABOVE> --secret | gpg --allow-secret-key-import --import

# Setup git ssh key
ssh-keygen -t ed25519 -C "benniemosher@gmail.com"
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
yay xclip
xclip -selection clipboard < ~/.ssh/id_ed25519.pub

# Setup dotfiles
mkdir -p ~/Code/
git clone git@github.com:benniemosher/dotfiles-linux.git ~/Code/dotfiles
rcup -v -d ~/Code/dotfiles -x .git -x README.md -x .gitignore -x bin

-- SKIP FOR NOW

# Install rbenv and ruby-build
# yay -S rbenv ruby-build
# rbenv init
# rbenv install 2.6.6
# rbenv global 2.6.6
# rbenv rehash

# Install Terraform
# yay -S tfenv
# sudo tfenv install 0.12.24
# sudo tfenv use 0.12.24

# Install gems needed for MOTD
# ruby --version # Should return 2.6.6, if not restart
# gem install lolcat artii cowsay
# yay -S fortune-mod

# yay -S visual-studio-code-insiders
# code --install-extension Shan.code-settings-sync
# code --enable-proposed-api Shan.code-settings-sync
# code .
# Login to Github and select the right gist
# `ctrl + shift + p` -> Sync: Download Settings

# Close and reopen Terminal

-- END SKIP FOR NOW

# Install and sign-in to multiple 1Password accounts
yay -S 1password # This is in beta, may require solo command

# Install slack and sign-in
yay slack-desktop # -S in this command currently gives broken install
# Open slack (bottom right quarter)

# Setup docker-compose
yay -S docker-compose
systemctl start docker
sudo groupadd docker
sudo usermod -aG docker ${USER}
# logout and back-in for above to take effects

# Setup github-cli
gh auth login

# Install and setup dropbox
yay dropbox # number 4
# If error about not being able to reach gpg server run below and retry install:
sudo pkill dirmngr
gpg --recv-keys 1C61A2656FB57B7E4DE0F4C1FC918B335044912E

# Install Brave Browser
yay -S brave
```
