# Django-Postgres-Gunicorn-Nginx-Docker
## 1. Develpment
Uses gunicorn 
### 1.1 Configuration
1. Rename *.env_dev_django-sample* to *.env_dev_django*.
2. Rename *.env_dev_db-sample* to *.env_dev_db*.
3. Check once, Database should have the same user,password and database's name in both .env_dev_django and .env_dev_db 

### 1.2 Build and Run the containers
``` sh 
    sudo docker-compose -f docker-compose.dev.yml up -d --build 
```
It builds and runs in dettached mode and check our webserver(django) at     [http://127.0.0.1:80](http://127.0.0.1:80)
### 1.3 Auto Update 
. The "backend" folder is mounted into the container and  code changes apply automatically.


### 2. Production

Uses gunicorn + nginx.
### 2.1 Configuration
1. Rename *.env_prod_django-sample* to *.env_prod_db* and *.env_prod_db-sample* to *.env_prod_db*. Update the environment variables.



2. Check once, Database should have the same user,password and database's name in both .env_prod_django and .env_prod_db 
### 2.2 Build and Run the containers
``` sh
docker-compose -f docker-compose.prod.yml up -d --build 
```
Test it out at [http://127.0.0.1:80](http://127.0.0.1:80). 

### 2.3 No auto update
No mounted folders. To apply changes, the image must be re-built.

### 2.4 Important commands
#### 2.4.1 Migrations
```sh
docker-compose -f docker-compose.prod.yml exec web python manage.py migrate --noinput
```
### 2.4.2 Collectstatic
```sh
docker-compose -f docker-compose.prod.yml exec web python manage.py collectstatic --no-input --clear
```

References: https://testdriven.io/blog/dockerizing-django-with-postgres-gunicorn-and-nginx/