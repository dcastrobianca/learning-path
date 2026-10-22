# Week 1: Linux VM

**Dates:** Oct 19 - Oct 23, 2026
**Status:** In progress

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
| Thu | nginx managed with systemd | Page loads from Windows; stops loading after `stop`; loads again after `start`; both events visible in the logs | Planned | `day-04-nginx.md` |
| Fri | Break it and fix it | Deliberate nginx config error found from tools, fixed and documented; this README reviewed | Planned | `day-05-break-and-fix.md` |

## What I learned

_To be completed at the end of the week._

- Key concepts:
- Commands I now know without looking them up:
- What I got wrong first:

## What broke and how I fixed it

_Filled in from the daily logs._

| Day | What broke | How I found it | Fix |
|---|---|---|---|
|  |  |  |  |

## Weekly review

_To be completed on Sunday._

- Planned outcomes met: _x of 5_
- Time spent: _hands-on / documentation_
- What to change next week:
