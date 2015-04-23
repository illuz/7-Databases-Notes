PostgreSQL Learning Notes
===


Doc: http://www.postgresql.org/docs/  
PostgreSQL Python tutorial: http://zetcode.com/db/postgresqlpythontutorial/  
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
[The cube module includes a GiST index operator class for cube values.](http://www.postgresql.org/docs/9.1/static/cube.html)  

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

---
*(Updating)*
