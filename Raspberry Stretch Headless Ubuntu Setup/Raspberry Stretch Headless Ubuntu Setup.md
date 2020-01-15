## Setting the Raspberry Pi Headless

* #### Source [One](https://medium.com/@aallan/setting-up-a-headless-raspberry-pi-zero-3ded0b83f274)

* #### Source [Two](https://medium.com/@DavidMaitland/raspberry-pi-zero-headless-setup-92fb72daf88d)



## SSH'ing Headless Raspberry Pi Through USB

* #### Install avahi and libnss-mdns in order to read hostname of device `sudo apt-get install avahi-daemon` & `sudo apt-get install libnss-mdns` (regardless it was not needed for this process since we search for the IP)

* #### Use `nmap -p22 127.0.1.1` in order to check the port state

* #### Use `nslookup raspberrypi.local` on terminal in order to search for the IP address of the hostname of device/server

* #### Once the IP  of the device is found, use sudo to ssh and -v for verbose printout of processes when ssh'ing `sudo ssh -v pi@127.0.1.1 `

* #### When dealing with port 22 error, install openssh-server with `sudo apt-get install openssh-server` and set port 22 as allowed `sudo ufw allow 22` 



## Alternative

* #### Change the network settings on the connectivity to the pi by changing the IPv4 Settings Method to Link-Local Only. For Instructions, go to `System Settings >> Network >> Second Listed Wired >> Options >> IPv4 Settings >> Method to Link-Local Only`. Afterwards give it a minute, once it notifies its connected, `sudo ssh -v pi@raspberrypi.local`. [Reference](https://raspberrypi.stackexchange.com/questions/71376/connecting-raspberry-pi-zero-to-ubuntu-computer-through-usb) to information   



## Setting up WiFi

* #### On the raspberry pi, go to `/etc/wpa_supplicant/wpa_supplicant.conf` and at the bottom of the file add 

  ```
  network={
      ssid="YOUR_SSID_HERE"
      psk="YOUR_SECRET_PASSPHRASE_HERE"
  }
  ```

  #### Afterwards run `sudo wpa_cli reconfigure` and reboot the pi to set the WiFi

  

## Installing Environment

* #### Install NodeJS and NPM in this [link](http://www.instructables.com/id/Install-Nodejs-and-Npm-on-Raspberry-Pi/). When unpacking node-v8.11.3-linux-armv6l.tar.gz use `tar xvf node-v8.11.3-linux-armv6l.tar.gz`

* #### An alternative to install NodeJS and NPM go to this [link](https://www.digitalocean.com/community/tutorials/how-to-install-node-js-on-ubuntu-16-04)

* #### For ZSH this [link](https://gist.github.com/tsabat/1498393)

* #### Sqlite Install is `sudo apt-get install sqlite3` 





### --- Reboot after all Installs, else you will get an npm error when running install ---



## Setting up TMUX

* #### Install Tmux `sudo apt install libavutil-dev tmux`

* #### Run `tmux` on terminal to start session. If responded with error `tmux: invalid LC<em>ALL, LC</em>CTYPE or LANG` run `sudo dpkg-reconfigure locales`

* #### If error keeps persisting, modify 'locale' file located at /etc/default/locale with command `sudo nano /etc/default/locale` and add/change to these commands 

  ```
  LANG=en_US.UTF-8
  LC_ALL=en_US.UTF-8
  LANGUAGE=en_US.UTF-8
  ```

* #### Sources - [Link1](http://techblog.danielpellarini.com/sysadmin/how-to-install-tmux-on-raspbian/) [Link2](https://raspberrypi.stackexchange.com/questions/43550/unable-to-reconfigure-locale-in-raspberry-pi)

  #### 

## Themes for TMUX

* #### [Source 1](https://github.com/gpakosz/.tmux)

* #### [Powerline for source 1](https://askubuntu.com/questions/283908/how-can-i-install-and-use-powerline-plugin)

* #### [Source 3](https://medium.com/@joe_wolfe_21/the-ultimate-terminal-67e93665459d)

* #### [A gentle introduction to tmux](https://hackernoon.com/a-gentle-introduction-to-tmux-8d784c404340)

  #### 

## Setting Glance	

* #### Install using `pip install glances`. [Source](https://nicolargo.github.io/glances/)

* #### If any errors with install, use `sudo /usr/bin/env python -m pip install glances` [Source](https://github.com/pypa/pip/issues/5221)

* #### If HTOP or Glance CPU in Tmux reads 100% at all times, this is the [reason](https://github.com/powerline/powerline/issues/1564). Follow up if you want to fix, will need to uninstall powerline

