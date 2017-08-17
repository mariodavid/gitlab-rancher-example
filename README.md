0. start / create docker-machine
- docker-machine status
- docker-machine start
- eval $(docker-machine env)

1. Start Gitlab

1.1 start Gitlab UI
- cat docker-compose.yml
- docker-compose up -d

1.2 start Gitlab runner
