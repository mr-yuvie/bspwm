<p align="center"><b>IMPORTANT:</b> Those who are looking for the old rice, it is on the worm branch, <a href="https://github.com/syndrizzle/hotfiles/tree/worm">click here</a> to check it out. </p>

<img alt="picture 2" src="https://i.imgur.com/hrNbdfD.gif" />  
<p align="center"><a href="#installation"><img alt="picture 2" src="https://i.imgur.com/Y7PKn7x.png" width="220"/></a><a href="#gallery"><img alt="picture 3" src="https://i.imgur.com/i9rmhBC.png" width="220"/></a><a href ="#support"><img alt="picture 1" src="https://i.imgur.com/LLIkH4D.png" width="220"/></a><a href="#credits"><img alt="picture 5" src="https://i.imgur.com/QA23l5X.png" width="220"/></a><a href="#tips"><img alt="picture 4" src="https://i.imgur.com/cg3KPZc.png" width="220"/></a></p>


<p align="center"><img src="https://img.shields.io/github/stars/syndrizzle/hotfiles?color=%231a1b26&label=STARGAZERS&labelColor=%231a1b26&style=for-the-badge"/>&nbsp;&nbsp;<img src="https://img.shields.io/github/forks/syndrizzle/hotfiles?color=%231a1b26&label=FORKS&labelColor=%231a1b26&style=for-the-badge"/>&nbsp;&nbsp;<img src="https://img.shields.io/github/issues/syndrizzle/hotfiles?color=1a1b26&labelColor=1a1b26&style=for-the-badge"/>&nbsp;&nbsp;<img src="https://img.shields.io/github/license/syndrizzle/hotfiles?color=1a1b26&labelColor=1a1b26&style=for-the-badge"/></p>

#### 1. ✨ The Bedazzle BSPWM ✨

### About:
* **Kitty** as the terminal.
* **Tokyo Night** as the color scheme.
* **BSPWM** as the window manager.
* **Picom (Fluffy Animations)** as the compositor.
* **EWW** as the widgets [Dashboard, Player and System Menu]
* **Rofi** as the application launcher.
* **Sddm** as the Display Manager.
* **Dunst** as the notification daemon.
* **Conky** as the desktop eyecandy.
* **jgmenu** as the desktop root menu.
* **Polybar** as the main bar.

⚠️ **NOTE!!!!!** This configuration is not owned by me, The original creater is [Syndrizzle](https://github.com/Syndrizzle). This is just my dotfiles after some tweaking for my personal usage. This was made for a **1920x1200** screen and on a **Laptop** with **96** dpi.

---
## Installation:
Below are the installation steps to install the dotfiles of my setup. Click on a step to Expand it.
<details>
<summary><b>1. Install Dependencies: </b></summary>

Before we begin the installation, you need to create a `Downloads` folder in your `/home` folder if it is not there by default.
```bash
mkdir ~/Downloads
```
Since we will store temporary cloned files in this folder.

For now the installation instructions are only provided for Arch Based distributions, I have not included the steps for others because I don't want to end up fighting with the compatibility issues on other distributions, I will add them after proper testing.<br>  

A one time command to install most of these dependencies with **your favorite AUR Helper** is given below, however some of them might need to be installed manually. In this case we are using yay, you can any other, I don't mind 🙃
```bash
yay -S kitty polybar rofi bspwm-rounded-corners-git xdg-user-dirs thunar xorg pavucontrol blueberry xfce4-power-manager feh lxappearance file-roller gtk-engines gtk-engine-murrine neofetch imagemagick parcellite xclip maim gpick curl jq tint2 zsh moreutils recode dunst plank python-xdg redshift mate-polkit xfce4-settings mpv yaru-sound-theme fish alsa-utils sddm xorg-xinit brightnessctl acpi mugshot playerctl python-pytz glava wmctrl i3lock-color jgmenu inter-font networkmanager-dmenu-git conky-lua bsp-layout zscroll noise-suppression-for-voice starship lsof gamemode lib32-gamemode xdo bluez bluez-utils bluez-libs bluez-tools
```

You also need `pylrc` which is a python module for handling the lyrics of song in the eww based player. You can skip this if you don't use spotify.
First install `pip`:
```bash
sudo pacman -S python-pip
```
Then:
```bash
sudo pip install pylrc
```
To install pylrc to your main `site-packages` folder.

Now you gotta install some dependencies which cannot be installed via the AUR helper/Pacman or it is better to install them this way:

#### 1. Eww
Elkowar's wacky widgets are the main widgets that we are gonna use in our system. It is a very essential dependency that you need.
First you need the nightly version of rust and also GTK3. A speedy way would be to directly install the binary package of rust nightly from the AUR using your favorite AUR helper:
```bash
yay -S rust-nightly-bin gtk3
```
Then we just need to run a few commands assuming you have `git` installed:
```bash
cd ~/Downloads
git clone https://github.com/elkowar/eww.git
cd eww
cargo build --release -j $(nproc)
cd target/release
sudo mv eww /usr/bin/eww
```
That installs eww to our root filesystem, which is then sourced from the `$PATH`.

#### 2. xqp
xqp comes from the author of `bspwm`.  It outputs the pointer ID under the window, basically, it is needed for the right click menu to function when clicking the root window in bspwm. The method of doing this was taken from [beyond9thousand](https://github.com/beyond9thousand)

NOTE: You need `base-devel` installed before this:
```bash
sudo pacman -S base-devel
```
Then you just gotta do:
```bash
cd ~/Downloads
git clone https://github.com/baskerville/xqp.git
cd xqp
make
sudo make install
```

#### 3. Picom Pijulius Fork
This picom fork has the best window animations you can get. For eyecandy we are using this fork, this isn't available in the AUR, so you need to install it manually:

First install all the dependencies required to build the compositor:
```bash
sudo pacman -S libconfig libev libxdg-basedir pcre pixman xcb-util-image xcb-util-renderutil hicolor-icon-theme libglvnd libx11 libxcb libxext libdbus asciidoc uthash
```
Then do the following:
```bash
cd ~/Downloads
git clone https://github.com/pijulius/picom.git
cd picom/
meson --buildtype=release . build --prefix=/usr -Dwith_docs=true
sudo ninja -C build install
```

Add your user to the ADM Group and start the following services:
```bash
sudo usermod -aG adm $USER
```

Bluetooth:
```bash
sudo systemctl enable bluetooth
```

With that, we have all the dependencies. We can move to the next part.
</details>
<details>
<summary><b>2. Installing GTK Theme:</b></summary>
To match with the current colorscheme, we are using the <a href="https://github.com/Fausto-Korpsvart/Tokyo-Night-GTK-Theme">Tokyo Night GTK Theme</a>

```bash
cd ~/Downloads
git clone https://github.com/Fausto-Korpsvart/Tokyo-Night-GTK-Theme.git
cd Tokyo-Night-GTK-Theme/
mv themes/Tokyonight-Dark-BL /usr/share/themes/
```
And that's it!
</details>
<details>
<summary><b>3. Installing Dotfiles:</b></summary>
The step we all have been waiting for.

Clone them and install:
```bash
cd ~/Downloads
git clone https://github.com/mr-yuvie/bspwm
cd bspwm
cp -r .config .scripts .local .cache .wallpapers ~/
cp .xinitrc .gtkrc-2.0 ~/
```
Install Fonts:
Assuming you are already in the `bspwm` folder
```bash
cd .fonts
mv * /usr/share/fonts
```
Move `sddm.conf` and `environment` to it's location:
Again assuming you are in the `bspwm` folder
```bash
cd etc/
mv sddm.conf environment /etc/
```
Copy items in `usr` folder to their respective places:
```bash
sudo cp -r usr/* /usr/
```
The usr folder contains the cursor theme and some executable scripts.

</details>

#### Miscllaneous:

<details>
<summary><b>Spicetify Theme: </b></summary>

Since we copied the dotfiles, we can apply the spicetify theme now.
First, install spicetify using:
```bash
yay -S spicetify-cli-git
```

Then, we need to give read and write access to our spotify folder for modifications:
```bash
sudo chmod a+wr /opt/spotify
sudo chmod a+wr /opt/spotify/Apps -R
```

After that we just need to run:

```bash
spicetify config current_theme Ziro
spicetify config color_scheme tokyonight
spicetify config extensions adblock.js
spicetify backup apply
```
This would install the spicetify theme to your Spotify.

</details>

<details>
<summary><b>Visual Studio Code Theme: </b></summary>
To get a consistent look for visual studio code, you can install the <b>Tokyo Night</b> Theme from the visual studio code marketplace.

[Click Here to access the theme link](https://marketplace.visualstudio.com/items?itemName=enkia.tokyo-night)

</details>

## Gallery:
<p align="center"><img src="https://i.imgur.com/EMuaeIv.png" width="1200"/></p>
<h3 align="center">The Desktop</h3>
<p align="center"><img src="https://i.imgur.com/9bwXOCm.png" width="1200"/></p>
<h3 align="center">The Main Dashboard</h3>
<p align="center"><img src="https://i.imgur.com/Zge2jbI.png" width="1200"/></p>
<h3 align="center">Spotify</h3>
<p align="center"><img src="https://i.imgur.com/n0oeBYP.png" width="1200"/></p>
<h3 align="center">A much better look at the desktop :)</h3>
<p align="center"><img src="https://i.imgur.com/arsPP2Q.png" width="1200"/></p>
<h3 align="center">Lock Screen using i3lock</h3>

## Tips:
### 1. Enable touchpad Tap-to-click:
If you are a laptop user, you might want to enable tap to click so that it gets easier to navigate using a touchpad. It is pretty easy to do so!
Copy and paste this one command in your terminal to fly!

```bash
sudo mkdir -p /etc/X11/xorg.conf.d && sudo tee <<'EOF' /etc/X11/xorg.conf.d/90-touchpad.conf 1> /dev/null
Section "InputClass"
        Identifier "touchpad"
        MatchIsTouchpad "on"
        Driver "libinput"
        Option "Tapping" "on"
EndSection

EOF
```

### 2. Enable GitHub Notification count.
If you are a GitHub user, you can get a notification count on your main bar.
For this you will need a **GitHub Personal Access Token** in order to authenticate yourself with the API.
[Follow this guide for obtaining the Personal Access Token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token)

Next, you just need to append the token to your polybar script using your preferred text editor, in this case we are using `nano` :
```bash
nano ~/.config/polybar/scripts/github
```
Now, replace `Your_Username` in the `USER` field with your GitHub username.
And then replace `Your_PAT` in the `TOKEN` field with your Personal Access Token.

### 3. Get your directories.
If there are no default directories when you do `dir` or `ls`, you might just have to manually create them.
Just install `xdg-user-dirs` and run the command, then reboot.
```bash
xdg-user-dirs-update
```

### 4. Turn on lock screen when you need it.
Since we are using xfce4-power-manager, we might want to make it toggle the lock screen when the laptop lid is closed, or if the laptop is just idle. To do this we can use `xfconf-query` to set the command that needs to manually toggle our lockscreen,
```bash
xfconf-query -c xfce4-session -p /general/LockCommand -s "$HOME/.scripts/lock" --create -t string
```
## Credits:

#### Thanks to:
*[Syndrizzle](https://github.com/Syndrizzle)

<p align="center"><b>That's it! Have a nice day!</b></p>
