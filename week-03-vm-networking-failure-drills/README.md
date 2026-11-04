# Week 3: Networking and failure drills on the Linux VM

**Dates:** Nov 2 - Nov 6, 2026
**Status:** In progress

## Goal

Put the expense app behind nginx as a reverse proxy, close the app's own port to outside traffic, back up and restore the database, and run network failure drills from Windows. By Friday the app is reachable only through nginx, I can restore the database from a backup, and I can tell a stopped app (502) from a stalled app (504) using the logs.

This is the second half of the manual deployment. Week 2 left the app running on the VM and reachable directly on port 8080, which is the gap this week closes.

By Friday I should be able to repeat the whole setup from my own notes.

## Environment

| Item | Value |
|---|---|
| Host | Windows 11 Home |
| Hypervisor | VirtualBox |
| Guest OS | Ubuntu Server (LTS) |
| VM network | Adapter 1: NAT (internet access). Adapter 2: Host-only (access from Windows). |
| New this week | nginx as reverse proxy, ufw firewall, pg_dump and pg_restore, nginx error log |

## Daily plan

Each session is 60 minutes: 10 minutes concept check, 40 minutes hands-on, 10 minutes of documentation, ending with a commit. Foundation reading, where needed, is done before the session.

| Day | Outcome | Done when | Status | Log |
|---|---|---|---|---|
| Mon | nginx runs as a reverse proxy in front of the app | From Windows, the app answers through nginx on port 80 | Done | `day-11-nginx-reverse-proxy.md` |
| Tue | The app's own port is closed to outside traffic | The app's own port is unreachable from Windows; the app still answers through nginx | Done | `day-12-firewall.md` |
| Wed | The database is backed up and restored | The database is restored from a dump; the app works afterwards | Done | `day-13-database-backup-restore.md` |
| Thu | Network failure drills | A stopped app returns 502, a stalled app returns 504, and the logs show each cause | Planned | `day-14-failure-drills.md` |
| Fri | Break it and fix it, week demo | After a VM reboot the app is back through nginx without a manual start; the README "On repeat" section repeats the whole setup | Planned | `day-15-week-demo.md` |

## Demo

_Fill in on Friday: from Windows, the app is reachable through nginx and not through its own port, and after a VM reboot it is back without a manual start._

## What I learned

_Fill in at the end of the week._

- Key concepts:
    * Firewall rules

        |Rule|	Direction|	Why it exists|
        |-|-|-|
        |allow ssh|	incoming |	Remote management of the VM|
        |allow 80 |	incoming |	Windows reaches the app through nginx|
        |default deny|	incoming|	Anything without an explicit allow is closed, including the app’s port 8080|
        |default allow|	outgoing|	The rate service and package updates need outbound access|
    * Database backup:

        How to use `pg_dump` to create a plain-text file of SQL statements that can be used to create a the database in the same state as it was at the time of the dump. It is stored in a simple sql file, and differently from a physical copy, can be used in newer versions of PostgreSQL and different system architecture. 
        
        Commands example:        
        * `pg_dump dbname > dumpfile`: create a backup file

        * `psql -X dbname < dumpfile`: applies the sql commands to recreate the database. 

        My VM:
        * Backup: `pg_dump -h localhost -U expense_app -d expense_app_db -f backup-<date>.sql` (use -h localhost, because the socket connection uses peer authentication and fails for this role).

        * Where: `/home/bianca/`, outside the PostgreSQL data directory.

        * Restore: `psql -X --set ON_ERROR_STOP=on expense_app_db_2 < backup-2026-11-04.sql -h localhost -U expense_app`


- Commands I now know without looking them up:
    * _pending_
- What I got wrong first:
    * _pending_

## On repeat

_Friday: list every command from Week 2 and Week 3 in order, so the setup can be rebuilt from this README._

## Weekly review

- Planned outcomes met: _pending_ of 5.
- What to change next week:
    * _pending_