![Diagram Overview](diagram/overview.png)

# Overview
This project allows you to quickly spin up a playground to test migration from multiple relational databases over to MongoDB by leveraging Relational Migrator.

## Disclaimer
The diagram above reflects the state of the Playground once fully complete. At this point in time however, the only source databases implemented are:

- MySQL
- Microsoft SQL Server
- PostgreSQL

# Getting started
## Setup / Start up
Getting started is as easy as:

- Cloning the repo
```
git clone git@github.com:bruno580/migrator-playground.git
```

- Download MySQL Connector and save it inside the "drivers" folder
Link: https://dev.mysql.com/downloads/connector/j/

- Running docker-compose
```
cd migrator-playground
docker-compose up -d
```

## Using Relational Migrator
You should now be able to access Relational Migrator by navigating to [http://localhost:8080](http://localhost:8080).

## Connecting to the databases
Each database is forwarding their default TCP ports onto their respective port in your local machine, therefore to connect to any databases from your localmachine, simply use any SQL client of your choice and connect to `localhost` on the specific default port for that database. **Important**: Because Relational Migrator is running from within a container itself, you will need to use the **container name** instead of `localhost`. Please refer to the table below for details.

| Database   | Hostname<br>(SQL Client) | Hostname<br>(Docker) | Port  | Username | Password            |
| ---------- | ------------------------ | -------------------- | ----- | -------- | ------------------- |
| MySQL      | localhost                | mysql-db             | 3306  | root     | root_password       |
| SQL Server | localhost                | sqlserver-db         | 1433  | sa       | YourStrongPassword! |
| MongoDB    | localhost                | mongodb-target       | 27017 | root     | example             |

**Example**: Based on the above table, this is what the connection string should look like for a migration job onto **mongodb-target**:
```
mongodb://root:example@mongodb-target:27017/demo?authSource=admin&authMechanism=SCRAM-SHA-256
```

## Data loading
When you bring the environment online, the databases are all empty. Feel free to use your sample schema of choice. A really basic example for MySQL can be [found here](https://github.com/bruno580/rm-query-converter-demo/blob/main/shopdb.sql).

## Stopping / Cleaning up
- To stop the containers, simply run:
```
docker-compose stop
```

- To remove the containers, run:
```
docker-compose down
```