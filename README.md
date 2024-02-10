# Steps to install

- mkdir ~/.config/awesome && cd !$
- git clone awesome wm widgets by [streetturtle](https://github.com/streetturtle/awesome-wm-widgets/) on github
- download [Arc icons](https://github.com/horst3180/arc-icon-theme#installation) for the battery widget
- copy each files from my dotfiles to their respective directories
- download dmenu
- download brave browser
- download i3lock
- download brightnessctl
    - use it without root permissions: sudo chmod +s $(which brightnessctl)
- git clone https://git.suckless.org/st ~/.config/st
    - common missing dependencies: libx11-dev libxft-dev build-essential


- make symbolic link from this repo to files-would-be location
```
ln -sf ~/dotfiles/tmux/tmux.conf ~/.config/tmux/tmux.conf
```
- download interception tools *from source* to remap CapsLock to Esc and Ctrl-L
- download caps2esc plugin
[tuto](https://askubuntu.com/questions/979359/how-do-i-install-caps2esc)
    - cmake, make, sudo make install
    - whereis udevmon
    - sudoedit /etc/udevmon.yaml
```
- JOB: intercept -g $DEVNODE | caps2esc | uinput -d $DEVNODE
  DEVICE:
    EVENTS:
      EV_KEY: [KEY_CAPSLOCK, KEY_ESC]
```
sudoedit /etc/systemd/system/udevmon.service
```
[Unit]
Description=udevmon
Wants=systemd-udev-settle.service
After=systemd-udev-settle.service

[Service]
ExecStart=/usr/bin/nice -n -20 /usr/local/bin/udevmon -c /etc/udevmon.yaml

[Install]
WantedBy=multi-user.target
```
```
sudo systemctl enable --now udevmon
```
