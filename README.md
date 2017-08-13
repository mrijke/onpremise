# Sentry On-Premise for Dokku

This repo is a fork of the official bootstrap for running your own [Sentry](https://sentry.io/) with [Docker](https://www.docker.com/).
This repo adds some [Dokku](http://dokku.viewdocs.io/dokku/) specific configuration so that you can run Sentry inside Dokku easily.

## Requirements

 * [Dokku](http://dokku.viewdocs.io/dokku/) installed and running

## Up and Running

Assuming you've just cloned this repository, the following steps
will get you up and running in no time!

### Install dokku plugins
On your Dokku installation, install the following plugins:

1) Install official **postgresql** plugin
```
sudo dokku plugin:install https://github.com/dokku/dokku-postgres.git postgres
```

2) Install official **redis** plugin
```
sudo dokku plugin:install https://github.com/dokku/dokku-redis.git redis

```

3) Install official **memcached** plugin
```
sudo dokku plugin:install https://github.com/dokku/dokku-memcached.git memcached
```

4) Install dokku letsencrypt plugin (if SSL is required)
```
sudo dokku plugin:install https://github.com/dokku/dokku-letsencrypt.git
```
### Configure Dokku
  * Create your app:
  ```
  dokku apps:create sentry
  ```
  * Create a PostgreSQL service
  ```
  dokku postgres:create sentry
  dokku postgres:link sentry sentry
  ```
  * Create a Redis service
  ```
  dokku redis:create sentry
  dokku redis:link sentry sentry
  ```
  * Create a Memcached service
  ```
  dokku memcached:create sentry
  dokku memcached:link sentry sentry
  ```
  * Set some config environment variables (secret key, SSL, email settings, see sentry.conf.py)
  ```
  dokku config:set sentry SENTRY_SECRET_KEY=... SENTRY_USE_SSL=1
  ```
### Deploying
In the directory of this cloned repo, add dokku as remote and deploy:
```
git remote add dokku dokku@dokku:sentry
git push dokku master
```
And everything should be deployed!
