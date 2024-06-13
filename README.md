Open a command terminal with current directory pointed at the repo.

To simulate a Nexus file, run each command in turn individually (to give time for it to complete):
1. docker compose --profile=broker up -d
2. docker compose --profile=start up -d
3. docker compose --profile=writer up -d
4. docker compose --profile=start up -d
5. docker compose --profile=stop up -d

To close, run:
docker compose --profile=all down