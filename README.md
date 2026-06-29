# STEMMechanics Website Docker Image

Docker build configuration for the STEMMechanics website.

This repository builds and publishes the production PHP container image used by the STEMMechanics Laravel website. The image is published to GitHub Container Registry and deployed through TrueNAS.

## Image

```text
ghcr.io/stemmechanics/stemmechanics-web:latest
```

## Purpose

This repository contains the Docker image definition for the website runtime environment.

It includes:

- PHP FPM
- Required PHP extensions
- Composer
- Node.js
- MySQL client tools
- Imagick support
- Laravel runtime dependencies

The Laravel application source currently lives separately at:

```text
https://github.com/stemmechanics/website
```

## Current Deployment Model

The Docker image provides the runtime environment.

The application files are mounted into the container on TrueNAS:

```text
/mnt/apps/website/app:/var/www/html
```

Runtime configuration is mounted separately:

```text
/mnt/apps/website/config/php.ini
/mnt/apps/website/config/nginx.conf
```

This allows PHP and nginx settings to be changed without rebuilding the Docker image.

## Build Locally

```bash
docker build -t ghcr.io/stemmechanics/stemmechanics-web:latest .
```

## Push to GHCR

```bash
docker push ghcr.io/stemmechanics/stemmechanics-web:latest
```

## GitHub Actions

This repository can use GitHub Actions to automatically build and publish the image when changes are pushed to `main`.

The image must remain public or TrueNAS must have valid GHCR credentials to pull it.

## Notes

This repository does not contain the Laravel application code.

It only defines the container runtime used to run the STEMMechanics website in production.
