[TYPO3 Docker Boilerplate](https://github.com/cysense-hq/docker-typo3)

Easy customizable TYPO3 Docker boilerplate for local development.

Supports:

* Apache HTTP Server 2.4.38
* PHP 7.3
* Xdebug 2.9.4
* MariaDB 10.1

## Installation without Composer

### Download TYPO3

```shell script
$ cd docker/php-apache
$ wget --content-disposition https://get.typo3.org/8.7.32
$ tar xzf typo3_src-8.7.32.tar.gz
$ rm typo3_src-8.7.32.tar.gz
```

### Environment variables

Create `.env` (copy from `.env.dist`) and modify.

```shell script
$ cp .env.dist .env
$ vim .env
```

### Local hosts file

Add `php-apache` service IP to local hosts file, e. g. like

```shell script
$ echo "172.20.1.3 typo3.docker" >> /etc/hosts
```

### Start Docker containers

Build and start the Docker containers with:

```shell script
$ docker-compose -f docker-compose.dev.yml up --build
```

### TYPO3 install tool

Open `http://typo3.docker/typo3/install.php`

Follow installation steps in [TYPO3 documentation - The Install Tool](https://docs.typo3.org/m/typo3/guide-installation/master/en-us/QuickInstall/TheInstallTool/Index.html)

Use database credentials of `.env` file and host `mariadb` and finish installation.

Installation done!

## Debugging

### Xdebug with PhpStorm

Step 1: __Set Xdebug port__

Open dialog Settings > Languages & Frameworks > PHP > Debug

Set Xdebug debug port to `10000`.

Step 2: __Add PHP server__

Open dialog Settings > Languages & Frameworks > PHP > Servers

Create server and set host to `typo3.docker`. Choose port `80` and debugger `Xdebug`.

Check `Use path mappings` and map following local project files/folders to absolute path on the server:

| Local file/folder | Absolute server path |
| --- | --- |
| `./docker/php-apache/typo3_src-8.7.32/typo3` | `/var/www/typo3_src-8.7.32/typo3` |
| `./docker/php-apache/typo3_src-8.7.32/vendor` | `/var/www/typo3_src-8.7.32/vendor` |
| `./docker/php-apache/typo3_src-8.7.32/index.php` | `/var/www/typo3_src-8.7.32/index.php` |

Step 3: __Start debugging__

Set breakpoint in PHP source code (e. g. in file `index.php`) and start debug connection (e. g. in menu `Run`, item `Start Listening for PHP Debug Connection`).

