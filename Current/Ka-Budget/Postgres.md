Initialize Postgres
- (Linux)
	start
	`sudo systemctl start postgresql`
	service status
	`sudo systemctl status postgresql.service`
	restart service
	`sudo systemctl restart postgres`
- (Manual Control)
	postgres user
	`sudo -i -u postgres`
	start the db (Needs the PGDATA env variable set correctly)
	`pg_ctl start`

Connecting to the Shell
- `sudo -u postgres psql`

Creating Databases
- `CREATE DATABASE name OWNER user;`

Creating Tables
- `CREATE TABLE table_name (
	`name varchar(80),
	`location point
	`);
	