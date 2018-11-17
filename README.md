# Laravel Docker Stack

A multi-stage, production-ready docker template for Laravel applications.

## Features
- Production-ready
- Optimised for build time &amp; size
- Frontend webpack asset compiling
- Backend composer requirements
- Ready to ship to a production cluster

## Requirements
- Laravel version `>=5.7`
- Docker version `>=17.05` (for multi-stage builds)

## How to use
1. Copy the `.docker` folder and `.dockerignore` into your project
2. Run `docker build -f .docker/Dockerfile .` and ship the image!
