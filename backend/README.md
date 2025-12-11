```shell
# Build
docker -f ./DockerfileOptimized build -t backend .

# Build with no cache (force fresh build)
docker build --no-cache -t backend .

# Run better compose
docker compose -f docker-compose.better.yml up -d

# Merge compose files
docker compose -f docker-compose.better.yml -f docker-compose.override.yml up -d

# Merge compose files and watch for changes
docker compose -f docker-compose.better.yml -f docker-compose.override.yml up --watch
```