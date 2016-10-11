# flasky-apcera-db

## Postgres Service Creation

    > apc service create flaskydb -p provider::/providers::your-pgsql-provider
    
## Service Binding to App

    > apc service bind flaskydb --job flasky-apcera-db

    ╭───────────────────────────────╮
    │ Binding Environment Variables │
    ├───────────────────────────────┤
    │ "FLASKYDB_URI"                │
    │ "JDBC_POSTGRES_URI"           │
    │ "POSTGRES_URI"                │
    ╰───────────────────────────────╯

The application (as configured in config.py) expects an environment variable named `POSTGRES_URI` of form `postgresql://username:password@hostname/database` by default.

## Application DB Schema Bootstrap
1. `apc app console flasky-apcera-db`
2. (in console) `cd /app; ./bin/python manage.py deploy`

## Application DB CRUD
1. `apc console create my-cap --image linux; apc service bind flaskydb --job my-cap`
2. (in capsule) `sudo apt-get update; sudo apt-get install postgresql postgresql-contrib`
3. (referencing `$POSTGRES_URI`) `psql --host=169.254.171.171 --port=20000 --username=6meuussqxamfohgv -d 5a1f124d272a42bb916dd5fd53ccd84a`
4. (manual email confirm) `update users set confirmed='t' where id=X;`
5. `\q` to exit psql...

## Flasky

This repository contains the source code examples for my O'Reilly book [Flask Web Development](http://www.flaskbook.com).

The commits and tags in this repository were carefully created to match the sequence in which concepts are presented in the book. Please read the section titled "How to Work with the Example Code" in the book's preface for instructions.

