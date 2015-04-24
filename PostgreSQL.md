PostgreSQL Learning Notes
===


Doc: http://www.postgresql.org/docs/  
PostgreSQL Python tutorial: http://zetcode.com/db/postgresqlpythontutorial/  
PostgreSQL Tutorial: http://www.tutorialspoint.com/postgresql/index.htm  
*<Seven Databases in Seven Weeks>*  

### Install

Souce code: http://www.postgresql.org/download/  

In Ubuntu:

```shell
# sudo apt-get update
# install postgresql
sudo apt-get install postgresql postgresql-contrib

# remove postgresql from start up scripts (just for learn not for use)
sudo update-rc.d -f postgresql remove
```

### Use it

Check, start and stop.

```shell
# check if is running
sudo /etc/init.d/postgresql status
sudo service postgresql status

# if not running, start it
sudo /etc/init.d/postgresql start
sudo service postgresql start

# stop it
sudo /etc/init.d/postgresql stop
sudo service postgresql stop
```

Create a new user (database role).

```shell

# login 'postgres'(default)
sudo -u -i postgres

# see all users
psql -c 'SELECT rolname FROM pg_roles;'

# create a super role for user 'illuz'
createuser -s illuz

# then you can login 'illuz' and operate databases
exit # exit the postgres
sudo -u -i illuz # login 'illuz'

# into Postgres prompt
psql

# exit prompt
\q
```


### Create Database
```shell
# after logining
createdb mydb
```

### Create Extension in the Database

Refer at this: http://stackoverflow.com/questions/1564056/how-do-i-import-modules-or-install-extensions-in-postgres-8-4  
([The cube module includes a GiST index operator class for cube values.](http://www.postgresql.org/docs/9.1/static/cube.html))  

```sql
# into Postgres prompt (psql)
# add extension 'cube'
CREATE EXTENSION "cube";
SELECT '1'::cube;   # test extension
```

### CRUD

#### Show help info

```sql
# into Postgres prompt (psql)
# show sql command info
\h CREATE INDEX;
# show psql command info
\?
```

#### Table

Most SQL is the same as MySQL...  

Some diff:  
- `SERIAL` is like `AUTO_INCREMENT` in MySQL.
- Use `RETURNING` to echo value.
- Use 'btree' to build index: `CREATE INDEX events_starts ON events USING btree(starts);`.

List:
- `\di` list indexes
- `\dt` list tables 
- `\du` list roles
- ... see in `\?`


### Window Function

Nice blog: [Understanding Window Functions](http://tapoueh.org/blog/2013/08/20-Window-Functions)  

### TRANSACTION

- BEGIN TRANSACTION: to start a transaction.
- COMMIT: to save the changes, alternatively you can use END TRANSACTION command.
- ROLLBACK: to rollback the changes.  

The ROLLBACK command can only be used to undo transactions since the last COMMIT or ROLLBACK command was issued.  

```sql
# into Postgres prompt (psql)
BEGIN;
DELETE FROM COMPANY WHERE AGE = 25;
ROLLBACK; # it will rollback and change anything
```

### String Match

#### In SQL

1. LILE, ILIKE
2. Regex: `~`(match), `!~`(un match), `~*`(ignore case)

#### Distance Match

Use `fuzzystrmatch` lib: `levenshtein(str1, str2)`.  

```sql
SELECT id, title FROM movies
WHERE levenshtein(lower(title), lower('day nigt')) <= 3;
```

#### Trigram

This will get all 'three continuous char'.  
Use `pg_trgm` lib: `show_trgm(str)`  

```sql
# test trigram
SELECT show_trgm('Avatre');

# use GIST[Generalized Index Search Tree] to create trigram index
CREATE INDEX movies_title_trigram ON movies
USING gist (title gist_trgm_ops);
```

#### metaphone

Match by pronounciation.  
Use `fuzzystrmatch` lib: `metaphone`

---
*(Updating)*
