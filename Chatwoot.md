# Database passwords

Postgres Details:-

- POSTGRES_HOST= postgres
- POSTGRES_DB=chatwoot
- POSTGRES_USER=postgres
// Please provide your own password.//
- POSTGRES_PASSWORD=Chatwoot!234


Redies Details:-

- REDIS_PASSWORD= Chatwoot!234

# Chatwoot Docker Deployment

## Tech Stack:

Posgresql: 5432
Redis: 6379
Ruby: 3000
React: 80

## download docker
```
sudo apt update
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
apt install docker-compose-plugin
```
## Download .env and docker compose files
```
wget -O .env https://raw.githubusercontent.com/chatwoot/chatwoot/develop/.env.example

wget -O docker-compose.yaml https://raw.githubusercontent.com/chatwoot/chatwoot/develop/docker-compose.production.yaml
```
## Update the passwords

### update redis and postgres passwords
vi .env

- REDIS_PASSWORD= Chatwoot!234
- POSTGRES_PASSWORD=Chatwoot!234
### update docker-compose.yaml same postgres pass
nano docker-compose.yaml

- POSTGRES_PASSWORD=Chatwoot!234

## Prepare the database by running the migrations.
```
docker compose run --rm rails bundle exec rails db:chatwoot_prepare
```
## Get the service up and running.
```
docker compose up -d
```
## Configure Nginx Reverse Proxy to access Chatwoot from Web

- sudo apt install nginx -y
- sudo rm -rf /etc/nginx/sites-enabled/default
- cd /etc/nginx/sites-available
- sudo vi chatwoot
```
# Configuration for chatwoot
server {
    listen 80;
    server_name chatwoot.murali.world;

    location / {
        proxy_pass http://localhost:3000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```
### Symlink of new configuration ( Soft link)
- sudo ln -s /etc/nginx/sites-available/chatwoot /etc/nginx/sites-enabled/
- sudo nginx -t
- sudo nginx -s reload
- sudo systemctl restart nginx
- curl http://chatwoot.murali.world

## Install SSL Certificate
- sudo apt install python3-certbot-nginx -y
- certbot --version
- sudo certbot --nginx -d chatwoot.murali.world
  - email: murali@digital-edify.com
  - redirect all traffic to https: 2

## Chatwoot Login Details

- visit: https://chatwoot.murali.world
- Username: Murali
- Email: murali@digital-edify.com
- Password: Amkamk3@













































