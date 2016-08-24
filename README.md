# flasky-paas-db

## Postgres Service Creation

    /Users/tbeets/Projects/learnPython/flasky-paas-db [git::master] [tbeets@tbeets-mac] [15:50]
    > apc provider list --namespace /
    Working in "/"
    ╭─────────────────────┬──────────┬─────────────────────────┬────────────────────────────────╮
    │ Name                │ Type     │ Namespace               │ Description                    │
    ├─────────────────────┼──────────┼─────────────────────────┼────────────────────────────────┤
    │ runq-uw2-priv-mysql │ mysql    │ /runq/providers/private │ MySQL RDS Instance: Private    │
    │ runq-uw2-priv-pgsql │ postgres │ /runq/providers/private │ Postgres RDS Instance: Private │
    ╰─────────────────────┴──────────┴─────────────────────────┴────────────────────────────────╯
    
    /Users/tbeets/Projects/learnPython/flasky-paas-db [git::master] [tbeets@tbeets-mac] [15:50]
    > apc service create flaskydb -p provider::/runq/providers/private::runq-uw2-priv-pgsql
    ╭────────────────────────────────────────────────────────────────────╮
    │                     Service Creation Settings                      │
    ├───────────┬────────────────────────────────────────────────────────┤
    │  Service: │ service::/runq/sandbox/tbeets::flaskydb                │
    │ Provider: │ provider::/runq/providers/private::runq-uw2-priv-pgsql │
    ╰───────────┴────────────────────────────────────────────────────────╯
    
    Is this correct? [Y/n]: Y
    Creating service... done
    Success!
    
    /Users/tbeets/Projects/learnPython/flasky-paas-db [git::master] [tbeets@tbeets-mac] [15:51]
    > apc service list
    Working in "/runq/sandbox/tbeets"
    ╭──────────┬──────────┬──────────────────────┬────────────────────────────────────────────────────────┬─────────────╮
    │ Name     │ Type     │ Namespace            │ Provider                                               │ Description │
    ├──────────┼──────────┼──────────────────────┼────────────────────────────────────────────────────────┼─────────────┤
    │ flaskydb │ postgres │ /runq/sandbox/tbeets │ provider::/runq/providers/private::runq-uw2-priv-pgsql │             │
    ╰──────────┴──────────┴──────────────────────┴────────────────────────────────────────────────────────┴─────────────╯
    
    /Users/tbeets/Projects/learnPython/flasky-paas-db [git::master] [tbeets@tbeets-mac] [15:51]

## Service Binding to App

    > apc service bind flaskydb --job flasky-paas
    ╭─────────────────────────╮
    │  Service Bind Settings  │
    ├───────────┬─────────────┤
    │ App Name: │ flasky-paas │
    │  Service: │ flaskydb    │
    ╰───────────┴─────────────╯
    
    Is this correct? [Y/n]: Y
    Binding service "flaskydb" to "flasky-paas"...
    Job must be stopped to bind to service. Do you want to stop it, apply the binding, and start it again?
    Restart and proceed? [Y/n]: Y
    Stopping job... done
    Creating binding... done
    Starting job... done
    Waiting for the job to start...
    [stderr] [2015-11-10 23:57:10 +0000] [3] [INFO] Starting gunicorn 19.3.0
    [stderr] [2015-11-10 23:57:10 +0000] [3] [INFO] Listening at: http://0.0.0.0:4000 (3)
    [stderr] [2015-11-10 23:57:10 +0000] [3] [INFO] Using worker: sync
    [stderr] [2015-11-10 23:57:10 +0000] [8] [INFO] Booting worker with pid: 8
    ╭───────────────────────────────╮
    │ Binding Environment Variables │
    ├───────────────────────────────┤
    │ "FLASKYDB_URI"                │
    │ "JDBC_POSTGRES_URI"           │
    │ "POSTGRES_URI"                │
    ╰───────────────────────────────╯
    Success!

The application (as configured in config.py) expects an environment variable named `POSTGRES_URI` of form `postgresql://username:password@hostname/database` by default.


## Flasky

This repository contains the source code examples for my O'Reilly book [Flask Web Development](http://www.flaskbook.com).

The commits and tags in this repository were carefully created to match the sequence in which concepts are presented in the book. Please read the section titled "How to Work with the Example Code" in the book's preface for instructions.

