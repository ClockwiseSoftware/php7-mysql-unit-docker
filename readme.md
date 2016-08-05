Container for using with Bitbucket Pipeline for testing Laravel project with PHPUnit
Using `php:latest` ( php7 )

Include MySQL 5.5, composer
and extending PHP with modules:
`iconv, mcrypt, gd, pdo_mysql, pcntl, pdo_sqlite, zip, curl, bcmath, opcacheб mbstring`

Example of `bitbucket-pipelines.yml`:
```yml
image: clockwise/php7-mysql-unit

pipelines:
  default:
    - step:
        script: # Modify the commands below to build your repository.
          - composer --version
          # copy default enviroment file
          - cp .env.example .env
          # install composer vendor scripts
          - composer install
          - vendor/bin/phpunit --version
          - mysql --version
          # start mysl
          - service mysql start
          # create default databese for project
          - mysql -u root -e "CREATE DATABASE kicker_chart"
          # migrate
          - php artisan migrate
          # run tests
          - vendor/bin/phpunit
```
