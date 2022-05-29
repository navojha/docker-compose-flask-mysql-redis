
# Web Application

This repository contains flask web application code. We can deploy it locally using docker-compose.
Once we execute this though docker-compose it will create three containers - application, Redis and MySQL database.
This is simple application and does not include scaling part. 

### Architecture

![Architecture](https://github.com/navojha/docker-compose-flask-mysql-redis/blob/main/Screenshots/Architecture.jpg)

          
    Backend application
        Model the following in the primary database
        i. Identifier
        ii. Name
        iii. Amount of gold 
    Application Endpoints
        a. Create player
            i. Store Identifier and Name in MySQL
            ii. Store Identifier and Gold in Redis
        b. Get player
            i. Retrieve Identifier and Name from the MySQL
            ii. Retrieve Gold from Redis 


## Table of Contents
    1. Getting started
    2. Local deployment
    3. Testing
### Getting started
#### Requirements
    Docker latest version should be installed on local machine.
#### Clone the repository 
    git clone https://github.com/navojha/docker-compose-flask-mysql-redis.git
    cd docker-compose-flask-mysql-redis

    $tree
     .   
    ├──Dockerfile
    ├──README.md
    ├──app.py
    ├──docker-compose.yml
    ├──requirements.txt
    └──templates
### Local deployment
     The entire stack - MySQL, Redis, and the backend application - will be deployable using docker-compose

    docker-compose up

    docker-compose ps

                    Name                                Command               State           Ports         
    ----------------------------------------------------------------------------------------------------------
    docker-compose-flask-mysql-redis_app_1     /bin/sh -c flask run --hos ...   Up      0.0.0.0:8083->8083/tcp
    docker-compose-flask-mysql-redis_mysql_1   docker-entrypoint.sh mysqld      Up      3306/tcp, 33060/tcp   
    docker-compose-flask-mysql-redis_redis_1   docker-entrypoint.sh redis ...   Up      6379/tcp              

### Testing
##### Create Player Table
localhost:8083
This will create the player table.
![Create Player Table](https://github.com/navojha/docker-compose-flask-mysql-redis/blob/main/Screenshots/Table_Created.png?raw=true)

##### Insert records in Player
    localhost:8083/Createplayer
    This End Point will use to enter the Player data.
![Insert records in Player](https://github.com/navojha/docker-compose-flask-mysql-redis/blob/main/Screenshots/Create_player.png?raw=true)

#### Player Created
![Player Created](https://github.com/navojha/docker-compose-flask-mysql-redis/blob/main/Screenshots/Player_created.png?raw=true)

#### Get Player Detail
    http://localhost:8083/Getplayer
    This endpoint will Retrieve Identifier and Name from the MySQL and Retrieve Gold from Redis. 
![Get Player Detail](https://github.com/navojha/docker-compose-flask-mysql-redis/blob/main/Screenshots/Get_Player.png?raw=true)

#### Logs 
    docker-compose logs
    Attaching to docker-compose-flask-mysql-redis_app_1, docker-compose-flask-mysql-redis_mysql_1, docker-compose-flask-mysql-redis_redis_1
    app_1    |  * Serving Flask app 'app.py' (lazy loading)
    app_1    |  * Environment: development
    app_1    |  * Debug mode: on
    app_1    |  * Running on all addresses (0.0.0.0)
    app_1    |    WARNING: This is a development server. Do not use it in a production deployment.
    app_1    |  * Running on http://127.0.0.1:8083
    app_1    |  * Running on http://172.24.0.4:8083 (Press CTRL+C to quit)
    app_1    |  * Restarting with stat
    app_1    |  * Debugger is active!
    app_1    |  * Debugger PIN: 543-812-981
    app_1    | 172.24.0.1 - - [25/May/2022 11:59:01] "GET / HTTP/1.1" 200 -
    app_1    | 172.24.0.1 - - [25/May/2022 11:59:02] "GET /favicon.ico HTTP/1.1" 404 -
    app_1    | 172.24.0.1 - - [25/May/2022 12:00:16] "GET /Createplayer HTTP/1.1" 200 -
    app_1    | 172.24.0.1 - - [25/May/2022 12:02:19] "POST /Createplayer HTTP/1.1" 200 -
    app_1    | 172.24.0.1 - - [25/May/2022 12:02:56] "GET /Getplayer HTTP/1.1" 200 -
    mysql_1  | 2022-05-25 11:57:46+00:00 [Note] [Entrypoint]: Entrypoint script for MySQL Server 8.0.29-1debian10 started.
    mysql_1  | 2022-05-25 11:57:47+00:00 [Note] [Entrypoint]: Switching to dedicated user 'mysql'
    mysql_1  | 2022-05-25 11:57:47+00:00 [Note] [Entrypoint]: Entrypoint script for MySQL Server 8.0.29-1debian10 started.
    mysql_1  | 2022-05-25 11:57:47+00:00 [Note] [Entrypoint]: Initializing database files
    mysql_1  | 2022-05-25T11:57:47.230440Z 0 [System] [MY-013169] [Server] /usr/sbin/mysqld (mysqld 8.0.29) initializing of server in progress as process 42
    mysql_1  | 2022-05-25T11:57:47.240011Z 1 [System] [MY-013576] [InnoDB] InnoDB initialization has started.
    mysql_1  | 2022-05-25T11:57:47.892188Z 1 [System] [MY-013577] [InnoDB] InnoDB initialization has ended.
    mysql_1  | 2022-05-25T11:57:49.202434Z 6 [Warning] [MY-010453] [Server] root@localhost is created with an empty password ! Please consider switching off the --initialize-insecure option.
    mysql_1  | 2022-05-25 11:57:52+00:00 [Note] [Entrypoint]: Database files initialized
    mysql_1  | 2022-05-25 11:57:52+00:00 [Note] [Entrypoint]: Starting temporary server
    mysql_1  | 2022-05-25T11:57:52.408220Z 0 [System] [MY-010116] [Server] /usr/sbin/mysqld (mysqld 8.0.29) starting as process 89
    mysql_1  | 2022-05-25T11:57:52.423657Z 1 [System] [MY-013576] [InnoDB] InnoDB initialization has started.
    mysql_1  | 2022-05-25T11:57:52.592959Z 1 [System] [MY-013577] [InnoDB] InnoDB initialization has ended.
    mysql_1  | 2022-05-25T11:57:52.811986Z 0 [Warning] [MY-010068] [Server] CA certificate ca.pem is self signed.
    mysql_1  | 2022-05-25T11:57:52.812098Z 0 [System] [MY-013602] [Server] Channel mysql_main configured to support TLS. Encrypted connections are now supported for this channel.
    mysql_1  | 2022-05-25T11:57:52.824450Z 0 [Warning] [MY-011810] [Server] Insecure configuration for --pid-file: Location '/var/run/mysqld' in the path is accessible to all OS users. Consider choosing a different directory.
    mysql_1  | 2022-05-25T11:57:52.849350Z 0 [System] [MY-011323] [Server] X Plugin ready for connections. Socket: /var/run/mysqld/mysqlx.sock
    mysql_1  | 2022-05-25T11:57:52.849878Z 0 [System] [MY-010931] [Server] /usr/sbin/mysqld: ready for connections. Version: '8.0.29'  socket: '/var/run/mysqld/mysqld.sock'  port: 0  MySQL Community Server - GPL.
    mysql_1  | 2022-05-25 11:57:52+00:00 [Note] [Entrypoint]: Temporary server started.
    mysql_1  | Warning: Unable to load '/usr/share/zoneinfo/iso3166.tab' as time zone. Skipping it.
    mysql_1  | Warning: Unable to load '/usr/share/zoneinfo/leap-seconds.list' as time zone. Skipping it.
    mysql_1  | Warning: Unable to load '/usr/share/zoneinfo/zone.tab' as time zone. Skipping it.
    mysql_1  | Warning: Unable to load '/usr/share/zoneinfo/zone1970.tab' as time zone. Skipping it.
    mysql_1  | 2022-05-25 11:57:55+00:00 [Note] [Entrypoint]: Creating database mydb
    mysql_1  | 2022-05-25 11:57:55+00:00 [Note] [Entrypoint]: Creating user myuser
    mysql_1  | 2022-05-25 11:57:55+00:00 [Note] [Entrypoint]: Giving user myuser access to schema mydb
    mysql_1  | 
    mysql_1  | 2022-05-25 11:57:55+00:00 [Note] [Entrypoint]: Stopping temporary server
    mysql_1  | 2022-05-25T11:57:55.512602Z 13 [System] [MY-013172] [Server] Received SHUTDOWN from user root. Shutting down mysqld (Version: 8.0.29).
    mysql_1  | 2022-05-25T11:57:56.398882Z 0 [System] [MY-010910] [Server] /usr/sbin/mysqld: Shutdown complete (mysqld 8.0.29)  MySQL Community Server - GPL.
    mysql_1  | 2022-05-25 11:57:56+00:00 [Note] [Entrypoint]: Temporary server stopped
    mysql_1  | 
    mysql_1  | 2022-05-25 11:57:56+00:00 [Note] [Entrypoint]: MySQL init process done. Ready for start up.
    mysql_1  | 
    mysql_1  | 2022-05-25T11:57:56.771131Z 0 [System] [MY-010116] [Server] /usr/sbin/mysqld (mysqld 8.0.29) starting as process 1
    mysql_1  | 2022-05-25T11:57:56.778536Z 1 [System] [MY-013576] [InnoDB] InnoDB initialization has started.
    mysql_1  | 2022-05-25T11:57:56.940217Z 1 [System] [MY-013577] [InnoDB] InnoDB initialization has ended.
    mysql_1  | 2022-05-25T11:57:57.113507Z 0 [Warning] [MY-010068] [Server] CA certificate ca.pem is self signed.
    mysql_1  | 2022-05-25T11:57:57.113576Z 0 [System] [MY-013602] [Server] Channel mysql_main configured to support TLS. Encrypted connections are now supported for this channel.
    mysql_1  | 2022-05-25T11:57:57.119678Z 0 [Warning] [MY-011810] [Server] Insecure configuration for --pid-file: Location '/var/run/mysqld' in the path is accessible to all OS users. Consider choosing a different directory.
    mysql_1  | 2022-05-25T11:57:57.142228Z 0 [System] [MY-011323] [Server] X Plugin ready for connections. Bind-address: '::' port: 33060, socket: /var/run/mysqld/mysqlx.sock
    mysql_1  | 2022-05-25T11:57:57.142249Z 0 [System] [MY-010931] [Server] /usr/sbin/mysqld: ready for connections. Version: '8.0.29'  socket: '/var/run/mysqld/mysqld.sock'  port: 3306  MySQL Community Server - GPL.
    redis_1  | 1:C 25 May 2022 11:57:46.784 # oO0OoO0OoO0Oo Redis is starting oO0OoO0OoO0Oo
    redis_1  | 1:C 25 May 2022 11:57:46.784 # Redis version=6.2.7, bits=64, commit=00000000, modified=0, pid=1, just started
    redis_1  | 1:C 25 May 2022 11:57:46.784 # Warning: no config file specified, using the default config. In order to specify a config file use redis-server /path/to/redis.conf
    redis_1  | 1:M 25 May 2022 11:57:46.785 * monotonic clock: POSIX clock_gettime
    redis_1  | 1:M 25 May 2022 11:57:46.785 # A key '__redis__compare_helper' was added to Lua globals which is not on the globals allow list nor listed on the deny list.
    redis_1  | 1:M 25 May 2022 11:57:46.785 * Running mode=standalone, port=6379.
    redis_1  | 1:M 25 May 2022 11:57:46.785 # Server initialized
    redis_1  | 1:M 25 May 2022 11:57:46.786 * Ready to accept connections
