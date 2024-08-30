```
version: "3.7"

services:
  runner:
    image: myoung34/github-runner:latest
    restart: always
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
    environment:
      RUNNER_SCOPE: repo
      RUNNER_NAME_PREFIX: myrunner
      LABELS: some-label
      REPO_URL: YOUR_REPO_LINK
      EPHEMERAL: 1
      ACCESS_TOKEN: YOUR_ACCESS_TOKEN
    deploy:
      replicas: 3
      resources:
        limits:
          cpus: '1'
          memory: 1G
        reservations:
          cpus: '0.2'
          memory: 256M

```
