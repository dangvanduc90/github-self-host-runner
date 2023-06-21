Tạo file docker-compose.yml và nên chạy riêng ở 1 server khác.
Lấy ACCESS_TOKEN từ trang github của quản trị viên, click vào avatar, Settings -> Developer Settings -> Personal Access Tokens > Token (Classic) > Generate New Token > Classic:

touch docker-compose.yml

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
      REPO_URL: https://github.com/dangvanduc90/github-self-host-runner 
      EPHEMERAL: 1
      ACCESS_TOKEN: <ACCESS_TOKEN>
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
