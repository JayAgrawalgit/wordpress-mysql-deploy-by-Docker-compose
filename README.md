# WordPress-MySQL-deploy-by-Docker-compose
Hello, Here we are using `Ubuntu 20.04.3 LTS` OS as a base machine.

### docker-compose.yaml file explain:
1. Here we are creating A web-Hosting setup on docker with the help of the docker-compose file.
2. For the docker-compose file we are using version 3.1
```yaml
version: '3.1'
```
3. Here for the frontend website display we are using WordPress and for the backend database, we are using MySQL.

```yaml
services:
  db:

  wordpress:

```
4. I am taking `mysql:5.7` as a database image and `wordpress:5.8` as the frontend image.
5. Here for both restart strategy will be `always`. 
6. MySQL need some environment like
```yaml
MYSQL_DATABASE: mysql_db
MYSQL_USER: db_user
MYSQL_PASSWORD: db_user_passwd
MYSQL_RANDOM_ROOT_PASSWORD: '1'
```
7. The same values go for WordPress also in its environment 
```yaml
WORDPRESS_DB_HOST: db
WORDPRESS_DB_USER: db_user
WORDPRESS_DB_PASSWORD: db_user_passwd
WORDPRESS_DB_NAME: mysql_db
```
8. we are storing MySQL & WordPress data from the locations 
```yaml
db: /var/lib/mysql
wordpress: /var/www/html
```
9. final output must be
```yaml
version: '3.1'

services:

  db:
    image: mysql:5.7
    restart: always
    environment:
      MYSQL_DATABASE: mysql_db
      MYSQL_USER: db_user
      MYSQL_PASSWORD: db_user_passwd
      MYSQL_RANDOM_ROOT_PASSWORD: '1'
    volumes:
      - db:/var/lib/mysql

  wordpress:
    image: wordpress:5.8
    restart: always
    ports:
      - 8080:80
    environment:
      WORDPRESS_DB_HOST: db
      WORDPRESS_DB_USER: db_user
      WORDPRESS_DB_PASSWORD: db_user_passwd
      WORDPRESS_DB_NAME: mysql_db
    volumes:
      - wordpress:/var/www/html

volumes:
  wordpress:
  db:

```
10. save this file name as a docker-compose.yaml
11. run below command to start the compose file
```bash
docker-compose up -d
```
12. now go to [http://localhost:8080/](http://localhost:8080/) to login to WordPress and have fun.
13. for taking down this compose file, run
```bash
docker-compose down
```
#### Keep Learning
