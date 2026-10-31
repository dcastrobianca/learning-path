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
| Tue | SSH key login from Windows to the VM | `ssh <vm>` logs in without a password prompt | Done | `day-02-ssh-key.md` |
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
    * NAT and Host-only adapter don't enable VM to receive request from internet.


## On repeat
1. Create VM in VirtualBox UI
2. Check system and network current config

    `ip a`

    `hostnamectl`

3. NAT adapter is already configured by default. Check VM access to internet

    `curl https://www.example.com`

4. Configure Host-only adapter
    * Power VM off
    * Add adapter from VirtualBox Ui settings:
        Ctrl+H -> create the adapter -> DHCP server enabled
    * Check new adapter, normally enp0s8. It was created but not configured yet, so VM is still not accessible from windows-machine. 

        `ip a`

    * Check network configuration : there should be just one file.

        `cd /etc/netplan/` + `ls -la`

    * Create a host-only configuration file.

        Files here works like building blocks and the higher the number, the latter it will be applied and could overwrite configurations done in previous files

        `sudo nano 01-host-only-adapter-config.yaml`

        ```yaml
            network:
                version: 2
                ethernets:
                    enp0s8:
                        dhcp4: true
                        addresses:
                            -   192.168.56.102/24
        ```

    * Test syntax for erros

        `sudo netplan generate`

    * Fix permission and test for erros again.

        `sudo chmod 600 01-host-only-adapter-config.yaml`

        `sudo netplan generate`

    * Apply netplan changes

        `sudo netplan apply`

5. Upgrade packages and clean up unnecessary one

    `sudo apt update && sudo apt upgrade`

    `sudo apt autoremove`

6. Check ssh service status. Shouldn't find one.

    `systemctl status ssh`

7. Install ssh server

    `sudo apt install openssh-server`

8. Check ssh service status again. it should be up and running.

     `systemctl status ssh`

9. Access VM from windows using ssh connection with password

    `ssh bianca@192.168.56.102`

10. Generate an ssh key-pair

    `ssh-keygen -f C:\Users\bianc\.ssh\my-key -t ed25519`

11. Add public key to VM

    * Access ssh key configured in my user 

        `cd .ssh`

    * Create a temporary file and paste public key.

        `nano pub-key.pub`

    * Append `authorized_keys` with temporary file content

        `cat pub-key.pub >> authorized_keys`

    * Access VM using private key.

        `ssh bianca@192.168.56.102 -i C:/Users/bianc/.ssh/my-key`
        
12. Create alias on windows machine to facilitate connection to VM

    * In .ssh add a config file:

        ```
            #Name used to connect
            Host linux-vm              
            HostName 192.168.56.102       
            IdentitiesOnly yes          
            IdentityFile ~/.ssh/my-key   
            User bianca
        ```
    * Access VM using alias

        `ssh linux-vm`

13. Config machine to accept key-pair only to login

    * Access config directory

        `cd /etc/ssh/sshd_config.d/`
        
    * Add config file
        `sudo nano 00-ssh-key-pair-login-only.conf`

        ```
            PermitRootLogin no
            PasswordAuthentication no
            KbdInteractiveAuthentication no
        ```
    * Restart ssh service

        `sudo systemctl restart ssh`

    * Try access VM with password only. It should return "Permission denied(publickey)"

        `ssh bianca@192.168.56.102`

    * Access VM with private-key. It should work

        `ssh bianca@192.168.56.102 -i C:/Users/bianc/.ssh/my-key`
        
14. Install Nginx and access web server from VM and from windows-machine.
    * Install 

        `sudo apt install nginx`

    * Check service status. Should be up and running

        `systemctl status nginx`

    * Test access from VM

        `curl localhost`

    * Test acccess from windows in browser

15. Stop and start service and check service-manager logs

    * Stop and check access in browser

        `sudo systemctl stop nginx`

    * Start and check access in browser

        `sudo systemctl start nginx`

    * Check service-manager logs

        `journalctl -u nginx`

16. Break Nginx config and see it in logs
    * Access file and introduce error

        `sudo nano /etc/nginx/nginx.conf`

    * Reload configuration and check that service is still available from browser

        `sudo nginx -s reload`

    * Restart service and see that service ins now unavailable

        `sudo systemctl restart nginx`

    * Check error

        `nginx -t`

        `journalctl -u nginx`
    
    * Fix config and restart service. Web server should be once again available

17. Create a clone of VM to be used on on-repeat session of week 2.


## Weekly review

- Planned outcomes met: 5 of 5.
- What to change next week:
    * more clear expected outcome and definition of done.
