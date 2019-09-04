# Retrive list of connections
select * from pg_stat_activity;

# execute command and exit
psql -c {cmd}

# Connect database
psql -d {db_name}

# List all databases
psql -l

# List roles and permission
\du

# List DB and owners
\l

# connect to db
\c {db_name}

# list tables in the connected DB
\dt

# List all columns in table
\d {tble_name}

# query extension installed in DB
SELECT name, default_version, installed_version, left(comment,30) As
comment
FROM pg_available_extensions
WHERE installed_version IS NOT NULL
ORDER BY name;

# select available extensions on the server
SELECT * FROM pg_available_extensions;
