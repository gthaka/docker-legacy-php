# Legacy PHP

[![GitHub issues](https://img.shields.io/github/issues/gthaka/docker-legacy-php.svg "GitHub issues")](https://github.com/gthaka/docker-legacy-php)

Given that some enterprises are a bit lethagic in maintaining / upgrading their systems, support and security updates eventually catch up with them. This is at least true based on experiences. Time is of the essence.
However, Docker to the rescure.

In this repo, I tackle this issue by for PHP legacy versions of a client who needed their old systems Dockerized for archiving.

## How to use this image

### Create a `Dockerfile` in your PHP legacy app project

```dockerfile
# specify the base image with your desired version gthaka/legacy-php:<version>
FROM gthaka/legacy-php:5.4
# replace this with your application's default port
EXPOSE 8000
```

You can then build and run the Docker image:

```console
$ docker build -t my-legacy-php-app .
$ docker run -it --rm --name my-old-app my-legacy-php-app
```

If you prefer Docker Compose:

```yml
version: "3"
services:
  legacy-app:
    image: gthaka/legacy-php:5.4
    working_dir: /var/www/html
    volumes:
      - ./:/var/www/html
    expose:
      - "8001"
```

You can then run using Docker Compose:

```console
$ docker-compose up -d
```

Docker Compose example mounts your current directory to the container.

- [Visit the Docker Repo here.](https://hub.docker.com/r/gthaka/legacy-php)

## Versions
Currently, only PHP 5.4 (5.4.45) has been created