# docker-compose-laravel
A simplified docker-compose workflow that sets up a network of containers for local Laravel development. You can view the full article that inspired the original repo [here](https://medium.com/@aschmelyun).

In this fork, I added PostgreSQL support and the possibility of adding multiple databases, which is useful for testing. I also addressed a problem that might occur to Linux hosts regarding permissions in the PHP container.

## Usage

To get started, make sure you have Docker and Docker-compose installed on your system, and then clone this repository.

Add your entire Laravel project to the `src` folder. If you're creating a new project from scratch on Linux, make sure to run the composer container with your host's uid:gid combination to avoid permission problems

```
docker-compose run --rm --user `id -u`:`id -g` composer create-project laravel/laravel .
```

then from this cloned respository's root run `docker-compose up -d --build`. Open up your browser of choice to [http://localhost:3000](http://localhost:3000) and you should see your Laravel app running as intended.

**New:** Three new containers have been added that handle Composer, NPM, and Artisan commands without having to have these platforms installed on your local computer. Use the following command templates from your project root, modifiying them to fit your particular use case:

- `docker-compose run --rm composer update`
- `docker-compose run --rm npm run dev`
- `docker-compose run --rm artisan migrate` 

Containers created and their ports (if used) are as follows:

- **nginx** - `:3000`
- **postgres** - `:5532`
- **php** - `:9000`
- **npm**
- **composer**
- **artisan**