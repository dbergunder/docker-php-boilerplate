# Docker PHP Boilerplate

- php: 7.4
- nginx: 3.11
- redis: 4

Docker boilerplate for quickly setting up a basic working php environment.  Database not included.  Feel free to modify for your own needs.

```dotenv
TIMEZONE=America/Chicago

# Basic symfony env var
APP_ENV=dev
APP_SECRET=4ed97b1ae17b2550a74e5bd20cdb7fa3

# Provide github token to composer for private repos
COMPOSER_AUTH='{"github-oauth":{"github.com":""}}'

WEB_PORT=8080
```

```bash
docker-compose up --build
```

```
http://localhost:8080
```