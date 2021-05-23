Gives you a quick local starting point for this free on demand tutorial.
https://courses.getdbt.com/collections

Documentation for DBT https://docs.getdbt.com/

# Install DBT

```
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

# Getting Started

Copy postgres profile from ./profiles.yml into your ~/.dbt/profile.yml

Start-up the postgres container db we're going to use (requires docker):
```
docker compose up
```

Note this will automatically execute the scripts that sets up the landing tables and source data.
The data is loaded from the tutorial csv's here `./data`
```
./data/db-init-scripts
```

Run DBT:
```
cd jaffle_shop
dbt run
```

you should see something like this:

```
Running with dbt=0.19.1
Found 3 models, 0 tests, 0 snapshots, 0 analyses, 138 macros, 0 operations, 0 seed files, 0 sources, 0 exposures

00:44:19 | Concurrency: 4 threads (target='dev')
00:44:19 | 
00:44:19 | 1 of 3 START view model dw.stg_customers............................. [RUN]
00:44:19 | 2 of 3 START view model dw.stg_orders................................ [RUN]
00:44:20 | 1 of 3 OK created view model dw.stg_customers........................ [CREATE VIEW in 0.13s]
00:44:20 | 2 of 3 OK created view model dw.stg_orders........................... [CREATE VIEW in 0.13s]
00:44:20 | 3 of 3 START view model dw.dim_customers............................. [RUN]
00:44:20 | 3 of 3 OK created view model dw.dim_customers........................ [CREATE VIEW in 0.07s]
00:44:20 | 
00:44:20 | Finished running 3 view models in 0.40s.

Completed successfully

Done. PASS=3 WARN=0 ERROR=0 SKIP=0 TOTAL=3
```

After successfully running DBT you should be connect to postgres:

```
username: jaffle_shop
password: jaffle_shop
database: jaffle_shop
server: localhost
port: 5432
```

DBT will have created 2 staging views used to comprise `dim_customers` in the schema `dw`:
```
dw.stg_customers
dw.stg_orders
dw.dim_customers
```

Run the the following to view `dim_customer`
```
SELECT * FROM dw.dim_customers
```

Proceed with the tutorial to see how to create and load tables, run tests and much more.

# Tear Down

```
docker compose down
```

# Reset the DB

```
docker compose down
rm -r ./data/postgres/*
```