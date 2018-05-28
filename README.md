# Factorio Headless Server with some bootstrapping


## Description

An ansible-playbook to bootstraping an ubuntu server and installing the factorio headless server.
https://wiki.factorio.com/Multiplayer#Dedicated.2FHeadless_server

### Software
python, fail2ban, ufw, factorio

### Firewall
policy: deny
open ports: OpenSSH, UDP 34197

### Tasks for bootstrapping
install python, update everything and restart

### Tasks for common
added users and groups, change ssh-config with no root-login, install and configure uwf and fail2ban, change hostname to domainname

### Tasks for factorio
added factorio user with passwordless sudo, download and unpack factorio in `/opt/factorio`, open UDP 34197, create systemd-file, create map and server config, create new map and start factorio


## Installation

1. change the hosts.example to hosts and add your host. the ansible script wants a domain, when you have no domain for your server please look at `role/common/taks/main.yml` at the task `change hostname` and below. You need change the Tasks or comment out. 
2. Optional: Check the fail2ban and sshd_config in `roles/common/templates` and make changes.
3. Add your users for the server with password an ssh-key. You need to crypt your password with `sha-512`.
4. Ready to rock! `ansible-playbook bootstrap.yml`.
5. `ansible-playbook common.yml`.
6. Change example files in `roles/factorio/files/` to your map and server settings.
7. `ansible-playbook factorio.yml`.
8. Let's Play!


## Usage

### Change Settings for factorio
You can change the map settings in `roles/factorio/files/map-gen-settings.json` and change the server settings in `roles/factorio/files/server-settings.json`.

### How to change the savegame
`ansible-playbook factorio_change_savegame.yml -e "new_savegame=foo old_savegame=bar"

### How to change the savegame
`ansible-playbook factorio_create_new_savegame.yml -e "old_savegame=bar"


## TODOs

Feel free and make Merge-Requests

1. Added variable "Version" for installing the right factorio version.
2. Maybe an update script is needed to update factorio, must be checked.
3. a new way for change hostname with domain and without.


## About Creators
42 N.E.R.D.S. a german softwaredeveloper and operations company. http://42nerds.com 

