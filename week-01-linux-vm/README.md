# Week 1: Linux VM

**Dates:** Oct 19 - Oct 23, 2026
**Status:** Done

## Goal

Build a Linux server from scratch, connect to it securely, run a web server on it, and practice fixing it when it breaks. This is the first stage of the path from physical or virtual server, to cloud, to containers, to Kubernetes.

By Friday I should be able to repeat the whole setup from my own notes.

## Environment

| Item | Value |
|---|---|
| Host | Windows 11 Home |
| Hypervisor | VirtualBox |
| Guest OS | Ubuntu Server (LTS) |
| VM network | Adapter 1: NAT (internet access). Adapter 2: Host-only (access from Windows). |

## Daily plan

Each session is 40 minutes of hands-on work and 10 minutes of documentation, ending with a commit.

| Day | Outcome | Done when | Status | Log |
|---|---|---|---|---|
| Mon | Ubuntu Server VM running | `hostnamectl` and `ip a` output recorded; VM survives a reboot; internet access and access from Windows confirmed | Done | `day-01-ubuntu-vm.md` |
| Tue | SSH key login from Windows to the VM | `ssh <vm>` logs in without a password prompt | Done | `day-02-ssh-keys.md` |
| Wed | VM accepts key-only ssh login | Root login is refused; A login attempt that skips the key is rejected without being offered a password; system updated | Done | `day-03-ssh-key-only-login.md` |
| Thu | nginx managed with systemd | Page loads from Windows; stops loading after `stop`; loads again after `start`; both events visible in the logs | Done | `day-04-nginx.md` |
| Fri | Break it and fix it | Deliberate nginx config error found from tools, fixed and documented; | Done | `day-05-break-and-fix.md` |

## What I learned


- Key concepts:
    * Difference of network adapter to connect to VM. NAT enable VM to access internet, Host-only creates a network to make VM accessible from my machine. 
    * Order of apt commands to upgrade system. 
    * SSH server and it's configurations.
- Commands I now know without looking them up:
    * `sudo service <service> start/stop/restart`
    * `sudo apt update && sudo apt upgrade`
    * `journalctl -u <service>`
    * `ssh <user>@<ip> -i ssh-private-key-file-path`
- What I got wrong first:
    * NAT and Host-only adapter don'e enable VM to receive request from internet.


## Weekly review

- Planned outcomes met: 5 of 5.
- What to change next week:
    * more clear expected outcome and definition of done.
