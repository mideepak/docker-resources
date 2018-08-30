## SonarQube with Docker

This is a Docker implementation of a SonarQube instance. This starts SonarQube 6.2 with MySQL 5.7 in a dockerized way.

The benefits of this over the traditional approach:
1. Easy to set up and tear down
2. Data and configuration external to containers
3. All the other advantages of using Docker containers over traditional application setup.

## Prerequisites

This needs to be run on a machine with
* Docker Engine v1.7.1 or later
* Any flavor of Linux


## How to run

All `docker-compose` commands *must be run* in the directory where `docker-compose.yml` is located.

To start the containers, do `docker-compose up`.
To kill existing containers, do `docker-compose kill`.

## Data Persistence

* *Check the `docker-compose.yml` file for the exact directories which are made persistent.*
* There is ample documentation on persistence of data for Docker containers. Go google!

Persistence of data across container restarts has been implemented by mounting a local directory as a volume into the container.

For SonarQube, the directory is **/opt/sonarqube_data**.
For MySQL, the directory is **/opt/mysql_data**.


## Notes and Gotchas

### SonarQube 6.2 and MySQL 8.0 do not work well

At the time of writing SonarQube 6.2 and MySQL 8.0 are the latest.
However some Sonar DB initialization commands throw MySQL Error 1064 on MySQL 8.0.

```
mysql> SELECT count(*) AS count_all FROM `group_roles` WHERE (role like 'default-%');
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use
```

*Downgrading to MySQL 5.7 works.*

### Connecting to the MySQL DB

To connect to the DB using MySQL client, first find out the IP of the MySQL Container:
[Link to StackOverflow Post](http://stackoverflow.com/a/20686101/682912)

Then do:

```
mysql -h [IP of MySQL Container] -u [username] -p
```
