# Microsoft SQL Server Sandbox
Sandbox setup as per the requirements by Clover Infotech team

### Install the MSSQL server (using Docker)
```sh
sudo docker run \
  -e "ACCEPT_EULA=Y" \
  -e "MSSQL_SA_PASSWORD=Strong@Passw0rd" \
  -p 1433:1433 \
  --name sql1 \
  --hostname sql1 \
  --detach \
  mcr.microsoft.com/mssql/server:2022-latest
```
### Monitor the MSSQL server running status
```sh
sudo docker ps -a
```
### Start the sqlcmd shell
```sh
sudo docker exec -it sql1 "bash"
```
### Create a new database
```sql
CREATE DATABASE TestDB;
SELECT Name from sys.databases;
USE TestDB;
GO
```
### Create the users table
```sql
CREATE TABLE users (
  id INT PRIMARY KEY AUTO_INCREMENT,
  first_name VARCHAR(50),
  last_name VARCHAR(50),
  designation VARCHAR(50),
  company_name VARCHAR(50)
);
```
### Insert 20 sample users
```sql
INSERT INTO users (first_name, last_name, designation, company_name) VALUES
  ('John', 'Doe', 'Manager', 'ABC Corp'),
  ('Jane', 'Doe', 'Engineer', 'XYZ Inc'),
  ('Bob', 'Smith', 'Developer', 'Acme Co'),
  ('Alice', 'Jones', 'Analyst', '123 Industries'),
  ('Mike', 'Johnson', 'Sales', 'Global Corp'),
  ('Samantha', 'Brown', 'Marketing', 'Sunset Enterprises'),
  ('David', 'Lee', 'Designer', 'Peak Performance'),
  ('Karen', 'Wilson', 'Programmer', 'Tech Solutions'),
  ('Chris', 'Taylor', 'Consultant', 'Enterprise Ventures'),
  ('Lisa', 'Green', 'Executive', 'Pacific Dynamics'),
  ('Mark', 'Davis', 'Researcher', 'Eagle Eye Innovations'),
  ('Sarah', 'Allen', 'Specialist', 'Innovative Ideas'),
  ('Brian', 'Baker', 'Coordinator', 'Peak Performance'),
  ('Susan', 'Collins', 'Administrator', 'United Co'),
  ('Kevin', 'Carter', 'Developer', 'Acme Co'),
  ('Emily', 'King', 'Manager', 'ABC Corp'),
  ('Jason', 'Miller', 'Designer', 'Peak Performance'),
  ('Linda', 'Scott', 'Programmer', 'Tech Solutions'),
  ('Tom', 'Clark', 'Analyst', '123 Industries'),
  ('Nancy', 'Turner', 'Consultant', 'Enterprise Ventures');
```
### Select all data from the users table
```sql
SELECT * FROM users;
```
### Run database integrity checks
```sql
USE TestDB;
DBCC CHECKDB;
DBCC CHECKALLOC;
DBCC CHECKCATALOG;
```
### Perform index maintenance
```sql
USE TestDB;
DBCC INDEXDEFRAG(0, users);
ALTER INDEX ALL ON users REORGANIZE;
ALTER INDEX ALL ON users REBUILD;
```
### Update table statistics
```sql
USE TestDB;
UPDATE STATISTICS users;
```
### Backup database
```sql
USE TestDB;
BACKUP DATABASE TestDB
TO DISK = 'C:\backup\TestDB.bak'
WITH COMPRESSION, COPY_ONLY;
```
### Restore database from backup
```sql
USE master;
RESTORE DATABASE TestDB
FROM DISK = 'C:\backup\TestDB.bak'
WITH REPLACE, RECOVERY;
```
&copy; Solution Enablers 2023. All rights reserved.
