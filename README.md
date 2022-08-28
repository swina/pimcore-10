# Pimcore Project Skeleton 

![Test Skeleton](https://github.com/swina/pimcore-10/actions/workflows/pimcore-skeleton.yml/badge.svg)

This skeleton should be used by experienced Pimcore developers for starting a new project from the ground up. 

## Docker

### Prerequisits

* Your user must be allowed to run docker commands (directly or via sudo).
* You must have docker-compose installed.
* Your user must be allowed to change file permissions (directly or via sudo).


### Run docker container (1st Run)

After cloning the repo:

1. Initialize the skeleton project using the `pimcore/pimcore` image (you can set my-project)

    ``docker run --rm -v `pwd`:/var/www/html pimcore/pimcore:PHP8.0-fpm composer create-project pimcore/skeleton my-project``

2. Go to your new project (or the name you set for my-project)

    `cd my-project/`

3. Create an .env.local file at the root of your project

    ```
    DB_HOST=db
    DB_NAME=pimcore
    DB_USERNAME=pimcore
    DB_PASSWORD=pimcore
    ```

4. Start the needed services with `docker-compose up -d`


5. Install pimcore and initialize the DB (only first run)

    `docker-compose exec php-fpm vendor/bin/pimcore-install --mysql-host-socket=db --mysql-username=pimcore --mysql-password=pimcore --mysql-database=pimcore`
    * When asked for admin user (admin) and password (pimcore) or choose freely

    
6. Enable Datahub bundle (used to create GraphQL Endpoints)

    `docker-compose exec php-fpm ./bin/console pimcore:bundle:enable PimcoreDataHubBundle`

    and

    `docker-compose exec php-fpm ./bin/console pimcore:bundle:install PimcoreDataHubBundle`

## Run docker (after 1st run)

Start the needed services with `docker-compose up -d`


## You can now visit your pimcore instance:
    * The frontend: <http://localhost:9000>
    * The admin interface, using the credentials you have chosen above:
      <http://localhost:9000/admin>


## Github Actions

Included is a basic github action to test 