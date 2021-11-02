# 🐳 Docker + PHP 7.4 + MySQL8.0 + Nginx + Certbot(HTTPS) + Symfony 5 Boilerplate 🐳

Edited from `https://github.com/ger86/symfony-docker` version -> `https://github.com/ger86/symfony-docker/tree/fc89a899ac58fb1f6ee5758377c001ad4ef4f389`

## Description

![docker_facebook_share](https://user-images.githubusercontent.com/57062736/139103227-36f3cb32-c3c1-4158-b99e-25a31e955f44.png)

This is a complete stack for running Symfony 5 into Docker containers using docker-compose tool and with Certbot for the HTTPS certificate.

It is composed by 4 containers:

- `nginx`, acting as the webserver.
- `php`, the PHP-FPM container with the 7.4 PHPversion.
- `db` which is the MySQL database container with a **MySQL 8.0** image.
- `certbot` generates the SSL certificate for your personal domain.

## Installation

![Docker Installation Illustration](https://user-images.githubusercontent.com/57062736/139102730-d6f51d53-ffb3-44bb-be5e-2bdf48d91295.png)

1. Clone this rep.

2. Check that the dir. `data/certbot/www/.well-known` exist. If it is not, create it 😀.

3. Edit `init` with your domain and an email.

4. Run `./init`.

5. Generate your Symfony proyecto goign to `/data/php/symfony` and running `composer create-project symfony/skeleton NAME_OF_THE_PROJECT`

6. Edit `data/nginx/web.conf` with your domain and youdr proyect dir.

7. Run `docker-compose down`

8. Run `docker-compose up -d`

9. The 4 containers are deployed: 

```
Creating docker_db_1      ... done
Creating docker_php_1     ... done
Creating docker_nginx_1   ... done
Creating docker-certbot-1 ... done
```

10. Remember to edit the `env` file at the root of the Symfony's project:

```
DATABASE_URL=mysql://db_user_name:db_user_pass@mysql:3306/db_name?serverVersion=5.7
```

## Docker's useful commands
![Docker Commands Illustration](https://user-images.githubusercontent.com/57062736/139102966-25f28be1-f768-49bd-a8a1-915a8465de9e.png)


- Run Docker-compose: `docker-compose up -d` / `docker-compose up`

- Check Docker-compose's volumens status: `docker-compose ps -a`

- Check Docker's images: `docker images -a`

- Remove Docker's images: `docker rmi -f imageID1 imageID2 ...` (-f = force)

- Enter to a Docker's volumen: `docker-compose exec VolumenID sh` / `docker-compose exec VolumenID bash`

- Copy a file to the docker we want to: `docker cp file docker_id:/dir`

- Remove all unused containers, volumes, networks and images: `docker system prune`
