# CakePHP and Docker Compose

This repo aims to be a one-stop-shop for getting cakephp up and running quickly with docker compose.

### prerequisites

 - [docker compose](https://docs.docker.com/compose/)
 - [composer](https://getcomposer.org/) (either installed locally or globally

### install

this will get the repo, install a blank cakephp, make a mysql-writable directory, and add a value to your `/etc/hosts` file so it is reachable.

```
git clone https://github.com/helloandre/cakephp-docker-compose
cd cakephp-docker-compose
composer create-project -q -n --prefer-dist cakephp/app cakephp/www
mkdir -p mysql/data
echo '127.0.0.1 cakephp.dev' | sudo tee -a /etc/hosts > /dev/null
```

### running

this will build the docker containers and start them.

`docker-compose up`

### database

your application will be available at `http://cakephp.dev:8080`. At first CakePHP will not be able to connect to the database, so you must update the values in `config/app.php`.

```
'Datasources' => [
    'default' => [
        'className' => 'Cake\Database\Connection',
        'driver' => 'Cake\Database\Driver\Mysql',
        'persistent' => false,
        // docker-compose manages this host
        'host' => 'cakephp_mysql_1',
        // defaults as set in docker-compose.yml
        'username' => 'cakephp',
        'password' => 'cakephp_password',
        'database' => 'cakephp',
        'encoding' => 'utf8',
        'timezone' => 'UTC',
        'flags' => [],
        'cacheMetadata' => true,
        'log' => false,
        'quoteIdentifiers' => false,
        'url' => env('DATABASE_URL', null),
    ],
],
```

if you wish to use any different credententials, you can change the values in `docker-compose.yml` and either connect to the container and change the values manually or (the nuclear apporach) delete the `mysql/data` directory.

### TODO

 - `bootstrap.sh` for easier setup/config
 - caching with `memcached`
