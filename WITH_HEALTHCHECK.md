# With HealthCheck

## Clone this repository.

## Create a `compose.yaml` with the following contents:

```yaml
services:
  muse:
    build: .
    restart: always
    healthcheck:
      test: curl -f http://localhost:8080/ || exit 1
      interval: 1m
      timeout: 10s
      retries: 3
      start_period: 1m
    volumes:
      - ./muse:/data
    environment:
      - DISCORD_TOKEN=
      - YOUTUBE_API_KEY=
      - SPOTIFY_CLIENT_ID=
      - SPOTIFY_CLIENT_SECRET=
  autoheal:
    restart: always
    image: willfarrell/autoheal
    environment:
      - AUTOHEAL_CONTAINER_LABEL=all
      # - WEBHOOK_URL=<DISCORD_WEBHOOK_URL>/slack
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
```

## Run `docker-compose up -d` to start the container.
