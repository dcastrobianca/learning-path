# Week 5: An Azure VM and the expense app running on it

**Dates:** Nov 16 - Nov 21, 2026 (sessions on Wed, Thu and Sat; the Monday and Tuesday sessions did not happen)
**Status:** In progress

## Goal

Create the first Linux VM in Azure, run the expense app on it the same way I ran it on the local VM, and put nginx and Azure network rules in front of it. By Wednesday I can reach a VM in my resource group over SSH from Windows. By Thursday the expense app runs on it as a systemd service with its own PostgreSQL database. By Saturday the app answers through nginx on the VM's public IP, its own port is closed by an Azure network security group (not by ufw), and I have written down what differs from the local VM.

Week 4 ended without a VM, because the Thursday session did not happen. The VM session therefore moved to Wednesday of this week, ahead of the expense app deployment.

I deallocate the VM at the end of every session to protect the free credit. Each session starts with a 10-minute concept check. Anything unfinished moves to Monday of week 6.

This is the same setup as weeks 2 and 3, in a different place. The point is to see which parts of the local VM carry over unchanged and which ones Azure replaces: the virtual disk and network adapters, the host-only network, the SSH key handling, and ufw.

## Environment

| Item | Value |
|---|---|
| Host | Windows 11 Home |
| Cloud | Azure subscription (free tier), used through the Azure portal |
| Region | North Europe, same as the resource group from week 4 |
| Azure VM | Ubuntu Server LTS, smallest size available, SSH key login |
| Local VM | The Ubuntu Server VM from weeks 1-3 stays off; its README is the guide for the Thursday session |
| New this week | A Linux VM in Azure, the resources created with it (disk, network interface, public IP, network security group), auto-shutdown, stop versus deallocate, network security group rules |

## Daily plan

Each session is 90 minutes: 15 minutes of foundation reading, 10 minutes of concept check, 55 minutes of hands-on work and 10 minutes of documentation, ending with a commit. Day numbers continue from week 4.

| Day | Outcome | Done when | Status | Log |
|---|---|---|---|---|
| Wed | A Linux VM running in my Azure resource group that I can reach over SSH from Windows, then stopped so it does not use my credit | 1) A Linux VM exists in my resource group, in the same region, with SSH key login. 2) I connect to it over SSH from Windows and run `hostnamectl`. 3) I name each resource created alongside the VM in the resource group. 4) The VM status is stopped (deallocated) and auto-shutdown is set. 5) The README documents what I did, what worked and what did not. | Planned | `day-19-azure-linux-vm.md` |
| Thu | The expense app running as a systemd service on the Azure VM, with its PostgreSQL database | 1) The VM is started and I connect over SSH. 2) PostgreSQL runs on the VM with the app's database and user. 3) The app runs as a systemd service and answers on its own port from the VM itself (curl). 4) The VM is deallocated at the end of the session. 5) The README documents what I did, what worked, what did not, and what differed from the local VM. | Planned | `day-20-expense-app-azure-vm.md` |
| Sat | The expense app reachable through nginx from Windows, its own port closed with an Azure network security group rule, and the differences from the local VM written down | 1) From Windows the app answers through nginx on the VM's public IP. 2) The app's own port is not reachable from Windows, blocked by the network security group and not by ufw. 3) SSH is allowed only from my own IP. 4) After a VM restart the app is back without a manual start. 5) The VM is deallocated at the end of the session. 6) The README lists what differs from the local VM. | Planned | `day-21-nginx-nsg-azure-vm.md` |

The Saturday block is used for practice this week instead of the usual "on repeat" rebuild.

Foundation reading, each done inside its session:

| Day | Reading |
|---|---|
| Wed | Microsoft Learn, "Quickstart: Create a Linux virtual machine in the Azure portal" (including connecting over SSH and cleaning up) |
| Thu | My own week 2 README (PostgreSQL, build and run by hand, systemd service with protected secrets). I note what I expect to be different on Azure before starting |
| Sat | Microsoft Learn, "Network security groups overview" (including the default rules and how priority works) |

## Demo

_To fill on Saturday: screenshots, each with one line on what it proves._

1. The VM connected over SSH from Windows, with the `hostnamectl` output
2. The resource group listing every resource created alongside the VM, and the VM shown as stopped (deallocated)
3. The expense app running as a systemd service on the Azure VM, answering `curl` from the VM itself
4. The app answering through nginx on the public IP from Windows, and the app's own port refusing the connection
5. The network security group rules: port 80 open, SSH restricted to my own IP

## What I learned

_To fill during the week._

- Key concepts:
    * 
- Portal paths and commands I now know without looking them up:
    * 
- What differs between the local VM and the Azure VM:
    * 
- What I got wrong first:
    * 

## On repeat

Portal steps and commands. The steps from weeks 2 and 3 are not copied here: the PostgreSQL, systemd and nginx steps are steps 1-15 and 17-19 of the "On repeat" list in `week-03-vm-networking-failure-drills/README.md`. This list holds the Azure steps and what changes in those commands. This week the Saturday block is used for practice, so the list is written down but not rebuilt from notes.

1. Create a Linux VM in the resource group, Ubuntu Server LTS, smallest size, SSH key login, inbound SSH only

    _menu path:_

2. Set auto-shutdown

    _menu path:_

3. Connect to the VM over SSH from Windows and run `hostnamectl`

    _command:_

4. List the resources created alongside the VM

    _menu path:_

5. Stop the VM so that it is deallocated, and check the status

    _menu path:_

6. Start the VM and connect again

    _menu path:_

7. Install PostgreSQL, build the app and run it as a systemd service (week 3, steps 1-15)

    _what changed on Azure:_

8. Put nginx in front of the app (week 3, steps 17-19)

    _what changed on Azure:_

9. Add a network security group rule for port 80 and restrict SSH to my own IP

    _menu path:_

10. Check from Windows that the app answers on port 80 and not on its own port

    _command:_

11. Restart the VM and check that the app is back without a manual start

    _command:_

## Weekly review

- Planned outcomes met: _pending_ of 3.
- What to change next week:
    * _pending_
