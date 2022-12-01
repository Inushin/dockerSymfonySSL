# 🐳 Docker + PHP 7.4 + MySQL8.0 + Nginx + Certbot(HTTPS) + Symfony 5 Boilerplate 🐳

![symfony_logo](https://user-images.githubusercontent.com/57062736/151140439-1c8af7c8-5905-4a6f-a846-d988643ee76f.png)

If you find this useful, remember about giving a start ⭐ to this repo or share it 🔁

Edited from `https://github.com/ger86/symfony-docker` version -> `https://github.com/ger86/symfony-docker/tree/fc89a899ac58fb1f6ee5758377c001ad4ef4f389`

## Description 📋

![docker_facebook_share](https://user-images.githubusercontent.com/57062736/139103227-36f3cb32-c3c1-4158-b99e-25a31e955f44.png)

This is a complete stack for running Symfony 5 into Docker containers using docker-compose tool and with Certbot for the HTTPS certificate.

It is composed by 4 containers:

- `nginx`, acting as the webserver.
- `php`, the PHP-FPM container with the 7.4 PHPversion.
- `mysql` which is the MySQL database container with a **MySQL 8.0** image.
- `certbot` generates the SSL certificate for your personal domain.

## Installation ⌨

![Docker Installation Illustration](https://user-images.githubusercontent.com/57062736/139102730-d6f51d53-ffb3-44bb-be5e-2bdf48d91295.png)

0. You need ****Docker**** and ****Docker-compose**** where you are going to launch this so, if you do not have it... click [HERE](https://github.com/Inushin/dockerSymfonySSL#installing-docker-docker-compose-and-composer) or go to the end of this `.md` ^^

1. Clone this rep.

2. Check that the dir. `data/certbot/www/.well-known` exist. If it is not, create it 😀.

3. Edit `init` with your domain and an email.

4. Edit the `docker-compose.yml` with your DB information. 

5. Run `./init`.

6. Generate your Symfony proyect going to the php container `docker-compose exec php bash`. Then, go to symfony folder, `/var/www/certbot/phpDir/symfony`, and run `composer create-project symfony/skeleton NAME_OF_THE_PROJECT`. If you need to install **Composer** click [HERE](https://github.com/Inushin/dockerSymfonySSL#installing-docker-docker-compose-and-composer) or go to the end of this `.md` ^^

7. Edit `data/nginx/web.conf` with your domain and your project dir.

8. Run `docker-compose down`

9. Run `docker-compose up -d`

10. The 4 containers are deployed: 

```
Creating docker_db_1      ... done
Creating docker_php_1     ... done
Creating docker_nginx_1   ... done
Creating docker-certbot-1 ... done
```

11. Remember to edit the `env` file at the root of the Symfony's project. `mysql` is the name of the container that has your database:
```
DATABASE_URL=mysql://db_user_name:db_user_pass@mysql:3306/db_name?serverVersion=5.7
```


## Docker's useful commands 📑
![Docker Commands Illustration](https://user-images.githubusercontent.com/57062736/139102966-25f28be1-f768-49bd-a8a1-915a8465de9e.png)


- Run Docker-compose: `docker-compose up -d` / `docker-compose up`

- Check Docker-compose's volumens status: `docker-compose ps -a` / `docker-compose ps`

- Check Docker's images: `docker images -a`

- Remove Docker's images: `docker rmi -f imageID1 imageID2 ...` (-f = force)

- Enter to a Docker's volumen: `docker-compose exec VolumenID sh` / `docker-compose exec VolumenID bash`

- Copy a file to the docker we want to: `docker cp file docker_id:/dir`

- Remove all dangling (not tagged or associated with a container) containers, volumes, networks and images: `docker system prune`

- Remove all unused containers and images with at least one container associated to them: `docker system prune -a`

- Shows all unused local images: `docker images ls -f dangling=true`

- Shows all unused local volumes: `docker volume ls -f dangling=true`

- Remove all local volumes not used by at least one container: `docker volume prune`

## Installing Docker, Docker-compose and Composer 🛠
![Docker-composer](https://user-images.githubusercontent.com/57062736/141182130-b8ed2d7a-9a68-4387-b838-ba0d44bb4e0e.png)

**Adjust the installation to your OS. Here you have the one for EC2(AWS) with CentOS**
#
- Docker installation

1. Download and install Docker: `yum install docker`

2. Gives permisions so you can run it everywhere: `usermod -a -G docker ec2-user`

3. Starts Docker's service: `service docker start`

4. Starts Docker's service each time you run the SO: `chkconfig docker on`
#
- Docker-compose installation

1. Download and install Docker-compose: `curl -L "https://github.com/docker/compose/releases/download/1.26.2/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose`

2. Make it executable from anywhere: `chmod +x /usr/local/bin/docker-compose`

3. Makes an direct access for docker-compose: `ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose`

4. Check the version and the installation: `docker-compose --version`

#
- Composer installation


1. Download and install Composer: `curl -sS https://getcomposer.org/installer | php`

2. Moves the config file to the composer dir: `mv composer.phar /usr/local/bin/composer`

3. Makes an direct access of `composer.phar` file: `ln -s /usr/local/bin/composer /usr/bin/composer`

## ⭐ Feedback and bugs 🐞

If you find any bug or just want to give your feedback (remember the ⭐ ^^), **Feel free to do it**. I am, as you, constantly learning and things change so quickly that... no one knows ^^

## Version control 📝

- 0.0.0 - Adding the Version Control zone - 08/02/2022
- 0.0.1 - Updated useful Docker commands - 10/02/2022
- 0.1.0 - Add new volume to NGINX with web files & Remove unneeded files and directories - 9/11/2022
