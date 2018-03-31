Heroku Rails Development with Docker
=====================================

This Docker image is intended to serve as a base for your Rails dev environment based on Heroku.


## Example Usage

### Dockerfile

All you need is to use this image as your base:

```dockerfile
FROM moonswitch/heroku-rails
```

### Docker Compose

Assuming you have a Rails app with the above Dockerfile in the root of the repo, you can setup a `docker-compose.yaml` file like this:

```yaml
services:
  db:
    image: postgres:10
    volumes:
      - postgresql-data:/var/lib/postgresql/data

  app:
    build: .
    depends_on:
      - db
      - cache
    volumes:
      - ./:/app/user
    environment:
      DATABASE_URL: 'postgres://postgres:@db:5432/postgres'
    ports:
      - 3000:3000
    command: bundle exec rails server
```

Then just run `docker-compose up` and visit `http://localhost:3000` in your browser.