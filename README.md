# pgAdmin4 Docker Setup

This project provides a Dockerized pgAdmin4 instance for managing PostgreSQL databases. It includes support for pre-configured server connections via a shared `servers.json` file.

## Quick Start

1. **Clone the repo
2. **Start pgAdmin4:**
   ```sh
   docker compose up -d
   ```
3. **Access pgAdmin4:**
   - Open [http://localhost:8080](http://localhost:8080) in your browser
   - Login with the credentials set in `docker-compose.yaml` (`PGADMIN_DEFAULT_EMAIL` and `PGADMIN_DEFAULT_PASSWORD`)

## Pre-configured Server Connections

- The `servers.json` file is mounted into the container so all users see the same database connections.
- If you add or update `servers.json`, you must remove the pgAdmin container and data volume for changes to take effect (see below).

## Resetting pgAdmin4 and Data Volume

pgAdmin4 stores its configuration (including server connections) in the data volume. If you add or update `servers.json` after the first run, you must remove the container and the volume to see changes:

```sh
docker stop pgadmin
# Remove the container
docker rm pgadmin
# Remove the data volume
docker volume rm pgadmin4_pgadmin-data
# Restart pgAdmin4
docker compose up -d
```

## Environment Variables
- `PGADMIN_DEFAULT_EMAIL`: Login email for pgAdmin4
- `PGADMIN_DEFAULT_PASSWORD`: Login password for pgAdmin4

## Notes
- If you manually connect to databases in pgAdmin4, those connections are stored in the data volume and are not shared via `servers.json`. This is not recommended
- To share connections, update `servers.json` and reset the container and volume as described above.
- For more info, see the [pgAdmin4 Docker documentation](https://www.pgadmin.org/docs/pgadmin4/latest/container_deployment.html).
