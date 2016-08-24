# flasky-apcera-db

## Postgres Service Creation

    > apc service create flaskydb -p provider::/providers::your-pgsql-provider
    
## Service Binding to App

    > apc service bind flaskydb --job flasky-paas

    ╭───────────────────────────────╮
    │ Binding Environment Variables │
    ├───────────────────────────────┤
    │ "FLASKYDB_URI"                │
    │ "JDBC_POSTGRES_URI"           │
    │ "POSTGRES_URI"                │
    ╰───────────────────────────────╯

The application (as configured in config.py) expects an environment variable named `POSTGRES_URI` of form `postgresql://username:password@hostname/database` by default.

## Flasky

This repository contains the source code examples for my O'Reilly book [Flask Web Development](http://www.flaskbook.com).

The commits and tags in this repository were carefully created to match the sequence in which concepts are presented in the book. Please read the section titled "How to Work with the Example Code" in the book's preface for instructions.

