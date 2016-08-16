Container for using with Bitbucket Pipeline for testing Laravel project with PHPUnit
Using PHP:latest ( php7 )

Include MySQL 5.5, composer
and extending PHP with modules:
iconv, mcrypt, gd, pdo_mysql, pcntl, pdo_sqlite, zip, curl, bcmath, opcacheб mbstring

Example of bitbucket-pipelines.yml:
```yml
image: clockwise/php7-mysql-unit

pipelines:
  default:
    - step:
        script: # Modify the commands below to build your repository.
          - composer --version
          - cp .env.example .env
          - composer install
          - vendor/bin/phpunit --version
          - mysql --version
          - service mysql start
          - mysql -u root -e "CREATE DATABASE kicker_chart"
          - php artisan migrate
          - vendor/bin/phpunit
          ```
