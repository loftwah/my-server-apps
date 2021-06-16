https://github.com/rnaga/wordpress-rest-admin

docker-compose.yml

```yaml
version: '3.5'

services:

  react:
    build:
      context: .
      dockerfile: Dockerfile
    restart: always
    ports:
      - 3000:3000
    volumes:
      - react:/app

  wordpress:
    build:
      context: .
      dockerfile: ./docker/Dockerfile-wp
    restart: always
    ports:
      - 80:80
    environment:
      WORDPRESS_DB_HOST: db
      WORDPRESS_DB_USER: root
      WORDPRESS_DB_PASSWORD: root
      WORDPRESS_DB_NAME: wordpress
    volumes:
      - wordpress:/var/www/html
    depends_on:
      - db

  db:
    image: mysql:5.7
    restart: always
    ports:
     - 8806:3306
    environment:
      MYSQL_DATABASE: 'wordpress'
      MYSQL_USER: 'wordpress'
      MYSQL_PASSWORD: 'wordpress'
      MYSQL_ROOT_PASSWORD: 'root'
      MYSQL_ROOT_HOST: '%'
    volumes:
      - db:/var/lib/db
    command: --default-authentication-plugin=mysql_native_password

volumes:
  react:
  wordpress:
  db:
  ```

  EXAMPLE
  https://github.com/rnaga/wordpress-rest-admin/tree/master/example
  https://developer.wordpress.org/rest-api/