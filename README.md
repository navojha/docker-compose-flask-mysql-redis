
# Flask Application

This repository contains flask application code. We can deploy it locally using docker-compose.
Once we execute this though docker-compose it will create three containers - application, Redis and MySQL database.
This is simple application and does not support scaling part. 
          
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
    Docker latest version should be installed in local machine.
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

                    Name                                Command               State           Ports         
    ----------------------------------------------------------------------------------------------------------
    docker-compose-flask-mysql-redis_app_1     /bin/sh -c flask run --hos ...   Up      0.0.0.0:8083->8083/tcp
    docker-compose-flask-mysql-redis_mysql_1   docker-entrypoint.sh mysqld      Up      3306/tcp, 33060/tcp   
    docker-compose-flask-mysql-redis_redis_1   docker-entrypoint.sh redis ...   Up      6379/tcp              

### Testing
##### Create Player Table
localhost:8083
This will create the player table.
![VPC Created](https://github.com/navojha/docker-compose-flask-mysql-redis/blob/main/Screenshots/Table_Created.png?raw=true)

##### Insert records in Player
    localhost:8083/Createplayer
    This End Point will use to enter the Player data.
![VPC Created](https://github.com/navojha/docker-compose-flask-mysql-redis/blob/main/Screenshots/Create_player.png?raw=true)

#### Player Created
![VPC Created](https://github.com/navojha/docker-compose-flask-mysql-redis/blob/main/Screenshots/Player_created.png?raw=true)

#### Get Player Detail
    http://localhost:8083/Getplayer
    This endpoint will Retrieve Identifier and Name from the MySQL and Retrieve Gold from Redis. 
![VPC Created](https://github.com/navojha/docker-compose-flask-mysql-redis/blob/main/Screenshots/Get_Player.png?raw=true)
