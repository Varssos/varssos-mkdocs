# Nextcloud with mariadb

1. Install docker
2. Create project directory with docker-compose.yml:
```bash
mkdir ~/nextcloud_docker
cd nextcloud_docker/
```
3. Fill `MYSQL_ROOT_PASSWORD` and `MYSQL_PASSWORD` in `docker-compose.yml` content:
```yaml
version: '2'

volumes:
  nextcloud:
  db:

services:
  db:
    image: mariadb:10.6
    restart: always
    command: --transaction-isolation=READ-COMMITTED --log-bin=binlog --binlog-format=ROW
    volumes:
      - db:/var/lib/mysql
    environment:
      - MYSQL_ROOT_PASSWORD=STRONGPASSWORD
      - MYSQL_PASSWORD=PASSWORD
      - MYSQL_DATABASE=nextcloud
      - MYSQL_USER=nextcloud

  app:
    image: nextcloud
    restart: always
    ports:
      - 8080:80
    links:
      - db
    volumes:
      - ./nextcloud/apps:/var/www/html/apps
      - ./nextcloud/config:/var/www/html/config
      - ./nextcloud/data:/var/www/html/data
    environment:
      - MYSQL_PASSWORD=PASSWORD
      - MYSQL_DATABASE=nextcloud
      - MYSQL_USER=nextcloud
      - MYSQL_HOST=db
```
4. Run docker:
```bash
docker-compose up -d
```
5. Edit `nextcloud/config/config.php` content adding:
```
0 => 'localhost:8080',
1 => '192.168.0.x:8080',
2 => 'your_domain:8080',
```
6. Restart docker:
```bash
docker restart nextcloud_docker-app-1
```

## How to completely remove all installed docker containers
```bash
sudo docker stop nextcloud_docker-app-1
sudo docker stop nextcloud_docker-db-1

sudo docker rm nextcloud_docker-app-1
sudo docker rm nextcloud_docker-db-1
```
