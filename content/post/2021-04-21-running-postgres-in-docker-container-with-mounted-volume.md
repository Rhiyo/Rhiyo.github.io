---
title: "Running Postgres in Docker Container With Mounted Volume"
date: 2021-04-21T21:18:59+09:30
Tags: ['tutorial','docker','postgres']
---

Docker containers are stateless, meaning that they are not gauranteed to keep data if restarted. However if we're using docker for a postgres database we want to be sure our data persists. Theoretically, we could just never stop the docker container, but issues outside of our control could happen such as crashes or power outages. We get around this problem by mounting a volume to our container and storing the data there.


# Why use docker?
Reading online, some people seem to think it's a silly idea to use a docker container for a database server, and they make good arguments. I am personally using it for a few reasons:
* Makes the set up process easier for me.
* Practice with using the docker ecosystem.
* Helps separate the postgres files from the rest of the system and feels more organized for me mentally.
* Easy to manage multiple server instances.
	* I'll usually create and destroy new servers as I go through a lot of different tutorials and testing with them as I learn. 


# The process...
Now for the step by step process of deploying a postgres server on docker with a mounted volume. You'll need to have [docker installed](https://docs.docker.com/get-docker/) and your terminal open ready to input commands. I'm using Pop_OS! but aside from system file paths commands should be OS agnostic.


## Creating the volume
```shell
docker volume create db_data
```
> Replace db_data with whatever name you like, just remember to also replace it in future commands.

This will create a volume that we can mount to any container. Check to see if the volume is created properly by finding it in the results of a `docker volume ls` command. This step can be skipped if you want to mount a folder on your system instead.

 
## Starting the docker container
```shell
docker run --name my_postgres -v db_data:/home/postgres/data -e POSTGRES_PASSWORD=password -e PGDATA=/home/postgres/data -d postgres
```
This will run the [postgres image](https://hub.docker.com/_/postgres) as a docker container with a volume mounted and the data stored on that volume. Any data stored in this volume will persist even if the container is ended, and can even be mounted by a new container that was instantiated from the same postgres image or even other instantiated containers. For example, if you wanted to upgrade to a new version of postgres.


### Explaining the individual parts of the command
```shell
--name my_postgres
```
This dictates the name of the running container, if you've ran the above command and then run `docker container ls` you should see it listed. *my_postgres* can be changed to anything you desire. If you would like to stop it (removing everything generated except for what was in the volume) run `docker stop my_postgres`.  To delete the stopped container, run `docker container rm my_postgres`.

```shell
-v db_data:/home/postgres/data
``` 
This links the `db_data` volume to the `/home/postgres/data` file location on the container.  The default container home directory username is *postgres* but the *data* directory on the container may be named anything you desire. Note, that if you would like to link it to a directory on your parent system rather than a docker volume, replace the volume with a directory on your pc. The parameter would then, for example, become: `-v /home/mypcusername/data:/home/postgres/data` if your OS is linux.

```shell
-e POSTGRES_PASSWORD=password -e PGDATA=/home/postgres/data
```
A `-e` will send an environment variable to the container, for the postgres docker image *POSTGRES_PASSWORD* is a required environment variable and is how you will connect to your superuser once the container is running. *PGDATA* tells postgres where it should store the database, and as such, should match the directory that you input for the latter part of the ```-v``` parameter. More environment variables can be found on the [postgres docker page.](https://hub.docker.com/_/postgres)

Finally, `-d` tells docker to run the container as daemon, meaning that you'll be able to keep using the terminal window you're in and manually stop the container. While `postgres` tells docker the image to instantiate into a container.


## Connecting to and managing your postgres container

If you don't change the default username of postgres using environment variables while starting up the container, your default superuser name will be *postgres*. 


### Managing postgres from within container
If you would like to send individual commands to your container, such as psql commands, you can use exec. However, you can also use this to enter the bash terminal of your container or even psql.
```shell
docker exec -it my_postgres bash
```

*my_postgres* should match the value of the `-name` parameter entered earlier. The above command will enter bash within your container, if you would like to directly into psql you can also use replace `bash` with `psql -U postgres` where postgres should match the superuser name.


### Connecting to postgres server from outside container
The container automatically opens the port ```5432``` for accessing the postgres server (the port can be changed using environment variables). However, a container by default, will use bridge networking, giving the container its own IP local to your host PC. To find this IP you can run:
```shell
docker inspect my-postgres | grep IPAddress
```
With *my-postgress* again being changed to the name you gave the container earlier. This should return some lines with one of them containing the IP of the container. However, if instead you would like to share the IP address of your host computer (and ports), add `--net="host"` after `docker run` while initializing the container.


### Managing postgres server from outside container
There are many options for managing a server but my preference is [dbeaver](https://dbeaver.io/). 

![Step 1.](/img/post/2021-4-21-running-postgres-in-docker-container-with-mounted-volume/step1.jpg)

If you've installed this software, click the *new connection* icon under file menu button on the top left of the window and then click PostgreSQL and next. 

![Step 2.](/img/post/2021-4-21-running-postgres-in-docker-container-with-mounted-volume/step2.jpg)

If you've left the network mode as bridging (the default), enter the IP address you found earlier as the host, however if you switched to host — enter *localhost*. The database name will match the username that was input as an envrionment variable, the default being *postgres*. The username again being the latter, with the password also being what you had input as an environment variable, with which I used *password* as an example.

![Step 3.](/img/post/2021-4-21-running-postgres-in-docker-container-with-mounted-volume/step3.jpg)

This should be enough information to connect, however one extra setting I like to tick is within the PostgreSQL tab, *Show all databases*. Click *Finish* once you've configured everything you want to.

![Step 4.](/img/post/2021-4-21-running-postgres-in-docker-container-with-mounted-volume/step4.jpg)

If all is well, you should now have a connection to the database in dbeaver and be able to manage it from said software as a superuser.


# To conclude
If you followed all the steps correctly and there were no mistakes with my instructions or on your end, you should now have a working postgres container with a volume (or local drive) mounted to it so data may persist. You can now delete or stop this container at any time and remount the data again, which is useful: 
* In case of a crash
* You want to painlessly update the postgres server.
* For running multiple server instances. 

You should also be able to easily enter the container itself to manage the postgres server or connect to it from outside the container. 

I recommend testing to see if your volume or host local drive are mounted by creating a new database (with dbeaver), removing the container and then starting a new container with and without mounting the volume, to see if the data persists. 

I hope this article was of help! 

