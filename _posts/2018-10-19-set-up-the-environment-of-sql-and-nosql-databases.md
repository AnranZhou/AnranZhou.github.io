---
layout: post
title: Set up the environment of SQL and NoSQL Databases
date: 2018-10-19 18:47
tag:
- MySQL
- Postgresql
- MongoDB
category: blog
author: Anran Zhou
description: This blog is used to record the setup of different databases.
---

## 1. Database Installation and User Managenment
### 1.1 Mysql

{% highlight shell %}
# installation
brew install mysql

# Version
mysql --version

# Login
mysqld // start the server
mysql -u root

# Create User and grant privileges
create user anran identified by '123';
grant all privileges on anrandb.* to 'anran'@'%';
flush privileges;

# delete user
drop user anran@'%';

# Update passwd
alter user 'anran'@'%' identified by '123456';
flush privileges;

# show grants of a user
show grants for 'anran';
{% endhighlight %}


### 1.2 Postgresql

{% highlight shell %}
# Installation
brew install postgresql;

# Login
pg_ctl -D /usr/local/var/postgres start && brew services start postgresql; // start the Postgres server
// The default user is `postgres`
// The default command line utility is `psql`
psql postgres;
// We can change the user using -U parameter
psql postgres -U anran;

# Logging into psql, executing the following SQL queries
# Version
select version();

# CRUD
// list all users
\du

// create a new user: create role
CREATE ROLE username WITH LOGIN PASSWORD 'quoted password' [OPTIONS]

// grant auth to a new user: alter role
ALTER ROLE patrick CREATEDB;

// change passwd
\password anran

// create db
CREATE DATABASE databasename;

// grant a user to a new database
GRANT ALL PRIVILEGES ON DATABASE postgres_test TO anran;

// rename a database
ALTER DATABASE anran RENAME TO super_anran;

// \list: lists all the databases in Postgres
// \connect: connect to a specific database
// \dt: list the tables in the currently connected database

# CLI Utilites
# User CRUD
createuser anran
dropuser anran

# Database CRUD
createdb anran -U anran
dropdb anran

{% endhighlight %}


### 1.3 MongoDB
{% highlight shell %}

# installation
brew install mongodb

# version
mongo --version

# Login
// create a folder to store the run time files
mkdir -p /data/db

// start the server
<path to binary>/mongod --dbpath <path to data directory>

// connect to the server
mongo --host 127.0.0.1:27017

# Operations
[Official Docs](https://docs.mongodb.com/manual/mongo/#working-with-the-mongo-shell)

{% endhighlight %}