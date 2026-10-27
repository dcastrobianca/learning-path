# Week 2: A realistic application on the Linux VM

**Dates:** Oct 26 - Oct 30, 2026
**Status:** In progress

## Goal

Run a small but realistic application on the VM I built in week 1: a Spring Boot service with a PostgreSQL database, an API key, a configuration file and a call to an external service. By Friday the application starts by itself after a reboot, keeps its data, keeps its secrets out of the repository, and I know how to find the cause when something fails.

This is the first half of the manual deployment. Week 3 adds nginx as a reverse proxy, a firewall, database backup and restore, and network failure drills.

By Friday I should be able to repeat the whole setup from my own notes.

## The application

A tiny expense service that converts amounts to EUR using current exchange rates. It exists to practice operations, not business logic.

- `POST /expenses` stores an expense and its EUR amount; `GET /expenses` lists them.
- Both endpoints require an `X-API-Key` header.
- `GET /actuator/health` reports the database state.
- Exchange rates come from the free Frankfurter API (no key, no cost).

I generate the application code with AI and review it myself against five points: no hardcoded secrets, real timeouts, behavior when the database is down at startup, a README that matches the configuration, and a short description of the port, the config location and the secrets. The specification and the prompt are in `day-07-generate-review-app.md`.

## Environment

| Item | Value |
|---|---|
| Host | Windows 11 Home |
| Hypervisor | VirtualBox |
| Guest OS | Ubuntu Server (LTS) |
| VM network | Adapter 1: NAT (internet access). Adapter 2: Host-only (access from Windows). |
| New this week | PostgreSQL, Java (LTS from the Ubuntu repositories), Maven, Frankfurter API |

## Daily plan

Each session is 40 minutes of hands-on work and 10 minutes of documentation, ending with a commit.

| Day | Outcome | Done when | Status | Log |
|---|---|---|---|---|
| Mon | PostgreSQL runs on the VM with its own database and user, reachable only from the VM | Service active and back after a reboot; the app's user can log in from the VM; a connection from Windows is refused; README names the database, the user and where the password is kept | Done | `day-06-postgresql.md` |
| Tue | The expense app is generated, reviewed and committed | Code and README in the repo; review notes cover the five points; I can explain in one paragraph how the app starts and what it needs | Done | `day-07-generate-review-app.md` |
| Wed | The app builds into one jar and runs by hand against PostgreSQL | Health shows the database up; an expense is stored with its EUR amount; a request without the key returns 401; with the external service unreachable, `POST` returns 502 and the app keeps running | Planned | `day-08-build-run-app.md` |
| Thu | The app runs as a systemd service under its own user | Active after a reboot; restarts after the process is killed; secrets file readable only by the service user and no secret in the repo or logs; request lines visible in `journalctl` | Planned | `day-09-systemd-service.md` |
| Fri | Break it and fix it, week demo | Three failures (PostgreSQL stopped, port already in use, wrong secrets file permissions) found from the logs and fixed; after a reboot the app is back and its data is still there; "On repeat" complete | Planned | `day-10-break-and-fix.md` |

## Demo

After a VM reboot the expense app is back without a manual start, and its data is still in the database.

## What I learned

- Key concepts:
    * 
- Commands I now know without looking them up:
    * 
- What I got wrong first:
    * 

## On repeat

To be written on Sunday's review session: every command, in order, so the setup can be rebuilt from this page alone. I redo ann week's work to create muscule memory. 