# Apache and PHP on Docker

This is a basic docker environment for PHP development.
It is not intended to use directly as it stands, but rather to extend it and create custom development environments.

It provides a pre-configured Apache (2.4) + mod_php (PHP 5.6) web server, based on Debian 8 (Jessie).
Apache is configured to run with the `docker` user. It is then preferred to place your PHP application in `/home/docker` and modify the default VHOST to access it.

The environment come with MySQL 5.5 (no root password, simply access it with `mysql -u root`) and MongoDB 2.4.
Are also included and some PHP extensions: apcu, mcrypt, intl, mysql, curl, gd, mongo, and xdebug (this last one comes deactivated, run `php5enmod xdebug` and restart Apache to enable it).

Apache, MySQL and MongoDB are all started when the container comes alive.
As the main process (PID 1) of the container is `Supervisord`, you can stop and restart the 3 of them as much as you want with the Debian `service` command:

```bash
    # For Apache
    service apache2 stop
    service apache2 start
    service apache2 restart
    
    # For MySQL
    service mysql stop
    service mysql start
    service mysql restart
    
    # For MongoDB
    service mongodb stop
    service mongodb start
    service mongodb restart
```

A few other tools are also provided: Vim, Git, Curl and Wget.

## How to use it?

### From Docker hub

You can directly pull this image from [Docker hub](https://hub.docker.com/r/carcel/apache-php/) by running:

```bash
    docker run -t -i -p 8080:80 -d --name apache-php carcel/apache-php
```

### From GitHub

Clone the repository, go inside the created folder, and build the docker image:

```bash
    docker build -t "apache-php" .
```

Then you can run a container like this:

```
    docker run -t -i -p 8080:80 -d --name apache-php apache-php
```

Access the URL `localhost:8080` with your web browser to check that the container works. You can also go inside the container with:

```bash
    docker exec -i -t apache-php /bin/bash
```

## License

This repository is under the MIT license. See the complete license in the `LICENSE` file.