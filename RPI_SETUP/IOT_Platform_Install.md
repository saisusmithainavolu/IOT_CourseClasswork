# IOT Platform Installation Tutorial #

## Prequisites ##
1. laptop on wifi
2. dietpi on RPI on wifi

## Steps to follow ##

1. SSH to the RPI using the command `ssh dietpi@[PI_IPADDRESS]`

2. To install the softwares go to Search Software tab in DietPi interface
   - Type mqtt, Hit OK and select `123 MQTT message broker`. Install by hitting the spacebar and selecting ok
   - Type node-red, Hit OK  and select `122  Node-RED: tool for wiring devices, APIs and online services`. Install by hitting the spacebar and selecting ok
   - Type postgre, Hit OK and  select `194  PostgreSQL: Persistent advanced object-relational database server`. Install by hitting the spacebar and selecting ok
   - Move curser to Install and tab to ok 
   - Hit OK if you see MQTT, Node-red and postgre and start the install
   
3. Reboot the pi on the command line using `reboot` command and ssh in again.

### Setup Postgres ###

Nowthat we already installed postgres, we will configure it now.

1. run on your pi ssh session

> sudo su postgres

2. Create a user 

> createuser pi -P --interactive

When prompted, enter a password and confirm it, select 'n' for superuser, and 'y' for the next two questions.

3. connect to Postgres using the shell and create a test database:

> psql

>  create database test;

4. Exit from the psql shell and again from the Postgres user by pressing `Ctrl+D` twice. You are now logged in as Pi-user.

> sudo su postgres

> psql test

5. Create a table, add data and retrieve the data using below commands

> create table people (name text, company text);

> insert into people values ('Larry Ellison', 'Oracle');

> insert into people values ('Scott Devine', 'VmWare');

> select * from people;

8. To make the postgre ready for node-red run plsql on your pi an alter the listen_address settings using:

>  sudo su postgres

>  psql test

>  ALTER SYSTEM SET LISTEN_ADDRESSES = '*';

  `Note:` This will allow your postgres to recieve ip traffic.  The system is now exposed since this allows anyone to connect.

  3. Go to the root console by hitting `ctrl+D` twice and run below command to restart the service

> dietpi-services restart postgresql

4. Use cat command to see the log to check if the service started up tcp services

> cat /var/log/postgresql/postgresql-13-main.log

 
### Setup NODE-RED ###

1.   Connect to node-red using RPI Static IPaddr found in CLIENTS page in your WI-FI admin Panel.

http://{YOUR_RPI_IPADDRESS}:1880

1. Install node-red-contrib-re-postgres in your ssh command line using:

npm install node-red-contrib-re-postgres

2. Restart node-red with the command

> dietpi-services restart node-red

3. Get back to Node-Red and Go to Manage Pallet 
4. In the Manage pallet go to Install and install node-red-contrib-postgresql
5. pull a postgresql node into a flow
      - postgresql node is found under `storage` category 
7. Double click on the node and configure a database instance
8. Pull in a trigger and template node and debug node and wire them as below


