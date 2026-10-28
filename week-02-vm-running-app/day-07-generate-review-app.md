# Day 07: Generate and review the app with Claude code

**Outcome:** The expense app is generated, reviewed against five points, and committed to the repo.
**Done when:** 
1) The code is in it's own repository: https://github.com/dcastrobianca/basic-expense-app

2) Your review notes cover the five review points. 
3) You can explain in one paragraph how the app starts and what it needs to run.

## What I did

1. Generated the code using Claude Code integrated with my VS Code Ui.
2. Create api-key
    * Create key: `setx EXPENSE_API_KEY "$(openssl rand -hex 32)"`
    * restart terminal and VS Code
    * Check if key was stored properly: `[ -n "$EXPENSE_API_KEY" ] && echo "set" || echo "missing"`

3. Create database in windows-machine
    * Install postgres in Windows. Windows Setup Wizard makes define superuser mandatory for instalation.
    * Enable psql CLI by adding bin folder to Path. Test with `psql --version`
    * Connect to DB server with superuser and used comands from day-06 to create dedicated user and database. 
        * `psql -U postgres -h localhost`
        * Create user and its password
        ```sql
            CREATE ROLE expense_app LOGIN NOSUPERUSER NOCREATEDB NOCREATEROLE;
            \password expense_app
        ```
        * Create database.
        ```sql
            CREATE DATABASE expense_app_db OWNER expense_app;
        ```

        As application will user Flyway, should not create tables manually, as it would generate conflict with the tool and would make the application not start. 

    * Add db password to system environment variables 

4. Start Application up
    * Send basic requests
        * GET /actuator/health
            ![health-get-request](day-07/day-07-health-request.png)

        * POST /expenses with valid parameters
            ![post-expense-valid](day-07/day-07-expense-post-request.png)

        * POST /expenses with invalid currency
            ![post-expense-bad-request](day-07/day-07-bad-request.png)
        * GET /expenses
            ![get-expense](day-07/day-07-expense-get-request.png)


5. 5 Review points
    1. No default passwords or keys anywhere.
        I only added system environment variables to configure api-key and db password. They are also not logged anywhere by the application.

    2. The timeouts really exist.

        ![timeout](day-07/day-07-timeout.png)

    3. What happens at startup when the database is unreachable.

        * Stop Postgres cluster 18 `net stop postgresql-x64-18` with app up and running

            ![stop-postgres](day-07/day-07-postgres-service-stop.png)

        * Send health request

            ![health-request-db-down](day-07/day-07-health-request-db-down.png)

            DB is showing as down, as app cannot establish connection to server.

        * Restart app with db server still unavailable, app doen't start.

            ![startup-fails-db-down](day-07/day-07-startup-db-down.png)

            Spring Boot applications that have Spring Data JPA will automatically look to create a database connection. 
            If it cannot establish this connection, the application will fail, unless it's configured otherwise. This is desired behabior, as without the database, the whole application functionality don't work. 


    4. The README matches the config variables in the code.

        |Config|README|Code|
        |-|-|-|
        |DB URL|jdbc:postgresql://localhost:5432/expenses|jdbc:postgresql://localhost:5432/expense_app_db|
        |DB user|expense|expense_app|
    

    5. You can state the port, the config location and the secrets in one paragraph.

        The minimum set up for running the application is Java 25, PostgreSQL with a database and user and an api-key. If one of those is nor provided, the application don't start. The default configurations are provided to the application using application.yaml, but the values comes from environment variables. Secrets don't have a default value, like api-key and database password. To know wich environment variables exists and can be changed, refer to application README file. 


## What worked
1. Preparing apps dependency before hand, like api key and install postgres server, while AI generated the code. This way, I optimized my time. I just had to change the configuration from my application after to match what I had configured.

## What did not work
1. I tried creating the tables for postgres db manually, and that made the application fail when starting. 

## How I solved it
1. I connected to database, dropped the table and restarted the application. 

## What I would do differently
1. Use a docker container to run the database would make it easier for future sessions, like "on repeat".  Revisit in the Docker weeks. 