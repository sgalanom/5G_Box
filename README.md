# 5G Core in VM

## Virtual Box Step-by-Step

- New VM 
  1) name: 5GinaBox
  2) folder: /home/sokra/VirtualBox/5GinaBox
  3) type: Linux
  4) version: Ubuntu 64-bit
  5) Memory size: 3GB
  6) Create virtual hard disk now
  7) `Create`

- `Start`

  Preinstall a driver and when prompted select it -> `ubuntu-24.04.2-desktop-amd64.iso`

- `Try or Install Ubuntu`
  1) Language
  2) Minimal installation and/or no updates or 3rd party
  3) Erase disk and install Ubuntu
  4) Time zone
  5) name: sokra
  6) computer's name: 5GinaBox
  7) password
- Wait for install
- `Restart now`
- Please remove, ... , press ENTER
- Devices > Insert Guest Additions CD image ...
- `Skip`
- Open disk, right click > Open in Terminal

  `sudo ./VBoxLinuxAdditions.run`

  If "*Please install ..*" -> `sudo apt-get install ..`. I had to do it for `bzip2 tar` and `gcc make perl`

  Do `sudo ./VBoxLinuxAdditions.run` until ok. `Then Power off machine`, `Start`
- For Copy/Paste

  Devices > Shared Clipboard > Bidirectional

  If it doesn't work, try `sudo VBoxClient --clipboard`. If this works, do `echo "VBoxClient --clipboard" >> ~/.bashrc`
- Display > Resolution > 1920x947 > `Apply`

READY

## Open 5GS Setup

- Look at Open5GS Cheatsheet [https://github.com/mohitkr05/5G_course/blob/main/open5gs/clickops/01_Open5GS_UeRANSIM/single_vm.md]

  `sudo apt-get update`

  `sudo apt-get install -y gnupg wget curl`
- For MongoDB

  `wget -qO - https://www.mongodb.org/static/pgp/server-6.0.asc | sudo apt-key add -`

  `echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu focal/mongodb-org/6.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-6.0.list`

  `sudo apt update`
  
  Try `sudo apt install -y mongodb-org mongodb-org-database`

  Use `sudo systemctl status mongod`. If the result is something like this,
  ```
    ● mongod.service - MongoDB Database Server
       Loaded: loaded (/usr/lib/systemd/system/mongod.service; enabled; preset: enabled)
       Active: active (running) since Thu 2025-03-27 13:28:09 EET; 3h 52min ago
         Docs: https://docs.mongodb.org/manual
     Main PID: 4343 (mongod)
       Memory: 59.1M (peak: 317.6M swap: 38.4M swap peak: 38.5M)
          CPU: 50.485s
       CGroup: /system.slice/mongod.service
               └─4343 /usr/bin/mongod --config /etc/mongod.conf
  
  Mar 27 13:28:09 5GinaBox systemd[1]: Started mongod.service - MongoDB Database Server.
  Mar 27 13:28:11 5GinaBox mongod[4343]: {"t":{"$date":"2025-03-27T11:28:11.080Z"},"s":"I",  "c":"CONTROL",  "id":7484500, "ctx":"-","msg":"Environment variable MONGODB_CONFIG_OVERRIDE_>
  ```
  you are ok

  Else follow instructions on Cheatsheet
- For NodeJs

  `curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -`

  `sudo apt install nodejs`
- For Open5GS

  `sudo add-apt-repository ppa:open5gs/latest`

  `sudo apt-get install -y software-properties-common`

  `sudo apt-get -y update && sudo apt install -y open5gs`

  Use `sudo service open5gs-* status`

  Check for Open5GS Daemon SMF, UPF, ...

  Use `ifconfig`, if necessary `sudo apt install net-tools`

  Then again `ifconfig`, check for **ogstun** network
- For WebUI

  `curl -fsSL https://open5gs.org/open5gs/assets/webui/install | sudo -E bash -`

  Find [Username: , Password: ]
- On Firefox, go to [http:/localhost:3000], or [http:/localhost:9999]
- Login to Open 5gs with username and password
