TYPO3 Docker Boilerplate

Easy customizable TYPO3 Docker boilerplate for local development

Supports:

* Apache HTTP server
* PHP 7.3
* MariaDB

## Installation

### Environment variables

Create `.env` (copy from `.env.dist`) and modify.

### Local hosts file

Add `php-apache` service IP to local hosts file, e. g. like

```shell script
$ echo "172.20.1.3 typo3.localhost" >> /etc/hosts
```

### Start Docker containers

Build and start the Docker containers with:

```shell script
$ docker-compose -f docker-compose.dev.yml up --build
```

## Debugging

### Xdebug with PhpStorm

Step 1: __Set Xdebug port__

Open dialog Settings > Languages & Frameworks > PHP > Debug

Set Xdebug debug port to `10000`.

Step 2: __Add PHP server__

Open dialog Settings > Languages & Frameworks > PHP > Servers

Create server and set host to `typo3.localhost`. Choose port `80` and debugger `Xdebug`.

Check `Use path mappings` and map local project file folder `./src/public` to absolute path on the server `/var/www/html`.

Step 3: __Start debugging__

Set breakpoint in PHP source code (e. g. in file `index.php`) and start debug connection (e. g. in menu `Run`, item `Start Listening for PHP Debug Connection`).

