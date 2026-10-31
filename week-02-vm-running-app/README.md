# Week 2: A realistic application on the Linux VM

**Dates:** Oct 26 - Oct 30, 2026
**Status:** Done

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
| Wed | The app builds into one jar and runs by hand against PostgreSQL | Health shows the database up; an expense is stored with its EUR amount; a request without the key returns 401; with the external service unreachable, `POST` returns 502 and the app keeps running | Done | `day-08-build-run-app.md` |
| Thu | The app runs as a systemd service under its own user | Active after a reboot; restarts after the process is killed; secrets file readable only by the service user and no secret in the repo or logs; request lines visible in `journalctl` | Done | `day-09-systemd-service.md` |
| Fri | Break it and fix it, week demo | Three failures (PostgreSQL stopped, port already in use, wrong secrets file permissions) found from the logs and fixed; after a reboot the app is back and its data is still there; "On repeat" complete | Done | `day-10-break-and-fix.md` |

## Demo

After a VM reboot the expense app is back without a manual start, and its data is still in the database.

## What I learned

- Key concepts:
    * Install and configured database. Create dedicated users with diferent permissions.
    * Difference between `postgresql.conf` and `pg_hba.conf`
    * Create a systemd service to run my application without manual intervation
    * Troubleshoot commom errors checking applications's log and status.
- Commands I now know without looking them up:
    * `sudo systemctl start/stop service-name`
    * `systemctl status service-name`
    * `journaltcl -u service-name --no-page -o cat -n ??`
    * `mvn package`
    * `sudo chown root:root /path/to/file`
    * `psql -h localhost -U user -d database`
    * `mkdir -p /complete/path`
    * `sudo reboot`
- What I got wrong first:
    * System environment variable configuration
    * systemd needing jar as executable. 

## On repeat

1. Install PostgreSQL

    `sudo apt update && sudo apt install postgresql`

    `psql --version`

2. Check postgre cluster

    `pg_lsclusters` - list clusters

    `systemctl status postgresql@18-main` - check status of cluster main of version 18

3. Reboot VM and check status

    `sudo reboot`

    `systemctl status postgresql@18-main`

4. Access database server with postgres superuser

    `sudo -u postgres psql`

5. Create database user

    `CREATE ROLE expense_app LOGIN NOSUPERUSER NOCREATEDB NOCREATEROLE;`

6. Define database user password 

    `\password expense_app`

7. Check users and permissions

    `\du`

8. Create database and set owner

    `CREATE DATABASE expense_app_db OWNER expense_app;`

9. List databases

    `\l`

10. Exit database server

    `\q`

11. Connect to database user it's user

    `psql -h localhost -U expense_app -d expense_app_db`

12. Print connection information

    `SELECT current_user, current_database();`

    `\conninfo`

13. Check use of port 5432

    `ss -tln | grep 5432`

14. Check access from windows machine to db server. Should fail because of PostgreSQL config `listen_addresses = localhost`

    `Test-NetConnection <vm-ip> -Port 5432`

15. Install Java
    
    `sudo apt upgrade && sudo apt install openjdk-25-jdk-headless`

    `java -version`

14. Install Maven
    
    `sudo apt install maven`

    `mvn -version`

15. Clone repository

    `git clone https://github.com/dcastrobianca/basic-expense-app.git`

16. Build jar

    * Access POM file folder

        `cd ~/basic-expense-app/expense-api`

    * Build jar

        `mvn package`

17. Create secret file

    * Create etc folder for service

        `sudo mkdir -p /etc/expense-api`

    * Create file with permission

        `sudo install -m 600 -o bianca -g bianca /dev/null /etc/expense-api/expense-api.env`

    * Add secrets to file

        `nano /etc/expense-api/expense-api.env`

        ```
            DB_PASSWORD_EXPENSE=my-db-password
            EXPENSE_API_KEY=my-api-key
        ```
18. Load secrets in every session

    `nano ~/.bashrc`

    ```
        set -a
        source /etc/expense-api/expense-api.env
        set +a
    ```

    `source ~/.bashrc`

19. Check environment variables without printing

    `[ -n "$EXPENSE_API_KEY" ] && echo set || echo missing`
    `[ -n "$DB_PASSWORD_EXPENSE" ] && echo set || echo missing`

20. Run app by hand

    `java -jar target/expense-api.jar`

21. Test app 
    * GET /actuator/health returns 200

        `curl localhost:8080/actuator/health`

    * POST /expenses returns 201

        `curl -X POST localhost:8080/expenses -H "X-API-Key: $EXPENSE_API_KEY" -H 'Content-Type: application/json' -d '{"description":"Lunch","amount":12.50,"currency":"USD"}'`

    * GET /expenses returns 200
        `curl localhost:8080/expenses -H "X-API-Key: $EXPENSE_API_KEY"`

    * GET /expenses without api-key returns 401

        `curl -i localhost:8080/expenses`

22. Create dedicated user to run app.

    `--system` creates an account meant for a service: a low user ID, and none of the normal-user defaults such as password aging.
    `--no-create-home` skips the home directory, since the service doesn’t need one.
    `--shell /usr/sbin/nologin` means nobody can log in as this user. It exists only so systemd can run the process under it.

    `sudo useradd --system --no-create-home --shell /usr/sbin/nologin expense-api`

23. Create application's file path and move jar file

    `sudo mkdir -p /opt/expense-api`

    `sudo mv ~/basic-expense-app/expense-api/target/expense-api.jar /opt/expense-api/`

24. Change permission from jar file: root-owned and world-readable

    `sudo chown root:root /opt/expense-api/expense-api.jar`

    `sudo chmod 644 /opt/expense-api/expense-api.jar`

25. Change file secret permission: owned, readable and writable by root only

    `sudo chown root:root /etc/expense-api/expense-api.env`

    `sudo chmod 600 /etc/expense-api/expense-api.env`

26. Make EXPENSE_API_KEY accessable

    `nano ~/.bashrc`

    Add to end of file and remove previos session `expense_key() { sudo grep '^EXPENSE_API_KEY=' /etc/expense-api/expense-api.env | cut -d= -f2-; }`

    With the change in permision from secret file, bashrc will not be able to access it whenerver the session is reload, as it was previously configure in step 18.

27. Create expense-api service definition

    `sudo nano /etc/systemd/system/expense-api.service`

    ```
        [Unit]
        Description=Expense API
        After=network.target postgresql.service

        [Service]
        User=expense-api
        EnvironmentFile=/etc/expense-api/expense-api.env
        ExecStart=/usr/bin/java -jar /opt/expense-api/expense-api.jar
        SuccessExitStatus=143
        Restart=on-failure
        RestartSec=5

        [Install]
        WantedBy=multi-user.target
    ```

    `After=` makes sure the app just start after network and PostgreSQL, to avoid a missing database error. `SuccessExitStatus=143` makes a SIGTERM stop count as a clean exit, as in the Spring page you read. `RestartSec=5` waits 5 seconds before restarting, so a crashing app can’t spin in a tight loop. `WantedBy=multi-user.target` is what enable hooks into, so the service starts at boot

28. Load service definition and start service

    `sudo systemctl daemon-reload`

    `sudo systemctl enable --now expense-api`

29. Check application status and logs before and after reboot

    `systemctl status expense-api`

    `journalctl -u expense-api -o cat`

    `sudo reboot`

    `systemctl status expense-api`

    `journalctl -u expense-api -o cat`

30. Test app. Use script from bashrc to retrieve expense-api-key. 

    * GET /actuator/health returns 200

        `curl localhost:8080/actuator/health`

    * POST /expenses returns 201

        `curl -X POST localhost:8080/expenses -H "X-API-Key: $(expense_key)" -H 'Content-Type: application/json' -d '{"description":"Lunch","amount":12.50,"currency":"USD"}'`

    * GET /expenses returns 200
        `curl localhost:8080/expenses -H "X-API-Key: $(expense_key)"`

31. Crash test
    `systemctl show -p MainPID --value expense-api`

    `sudo kill -9 <pid>` to end service abruptly

    `systemctl status expense-api`

    `journalctl -u expense-api -o cat`

32. Set timezone

    Logs shows time in UTC. I want to see it in local time.

    `sudo timedatectl set-timezone Europe/Berlin`

33. Test app with database down
    * Deactivate cluster
        `sudo systemctl stop postgresql@18-main`

        `systemctl status postgresql@18-main`

    * GET /health with response time

        `curl -i localhost:8080/actuator/health -w '\n%{time_total}s\n'`

    * POST /expenses request

        `curl -i -X POST localhost:8080/expenses -H "X-API-Key: $(expense_key)" -H 'Content-Type: application/json' -d '{"description":"Test","amount":5,"currency":"USD"}' -w '\n%{time_total}s\n'`

    * Check status and logs.

        `systemctl status expense-api` : should show running

        `journalctl -u expense-api -o cat -n 25`: should show connection refused error.

    * Restart PostgreSQL cluster and check status and logs

        `sudo systemctl start postgresql@18-main`

        `systemctl status postgresql@18-main`

        `curl -i localhost:8080/actuator/health -w '\n%{time_total}s\n'`:db status should be up.

34. Test app with busy port
    * Stop app service

        `sudo systemctl stop expense-api`

    * Use port (use new session)

        `nc -l 127.0.0.1 8080`

        `ss -tlnp | grep 8080`


    * Start app service

        `sudo systemctl start expense-api`

    * Check status and logs

        `systemctl status expense-api` : should show activation

        `journalctl -u expense-api -o cat -n 30`: should show port 8080 already used. Application cannot completly start and keeps retrying.

    * Free port and check logs

        `journalctl -u expense-api -o cat -n 50 --no-page`

35. Test app with jar file wrong permission

    * Change jar permission: only root has access.  

        `sudo chmod 600 /opt/expense-api/expense-api.jar`

    * Check app's user access to file.

        `sudo -u expense-api test -r /opt/expense-api/expense-api.jar && echo readable || echo not readable`

    * Restart service

        `sudo systemctl restart expense-api`

    * Check service status and logs

        `systemctl status expense-api`: should show activating

        `journalctl -u expense-api -n 15 --no-pager`: should show jar file unaccessible error. 

    * Fix jar file permission

        `sudo chmod 644 /opt/expense-api/expense-api.jar`

    * Check status. Should be running.

        `systemctl status expense-api`

36. Check app and persistance after reboot

    * Run GET /expenses request

        `curl localhost:8080/expenses -H "X-API-Key: $(expense_key)"`
    * Reboot VM

        `sudo reboot`

    * Run GET /expenses request. should be same as previous from reboot.

        `curl localhost:8080/expenses -H "X-API-Key: $(expense_key)"`

37. Create a clone of VM to use on on-repeat session of week 3. 






    
    

    






