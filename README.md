# PostgreSQL Docker Template

A simple Docker setup for running a PostgreSQL database.

## Setup

1. Update the files in the `secrets-example` directory with your desired credentials.

2. Rename the `secrets-example` directory to `secrets`.

3. Create the Docker network:

```bash
docker network create postgres-network
```

4. Start the PostgreSQL container:

```bash
docker compose up -d
```

> If the port is already in use, change the `POSTGRES_HOST_PORT` variable in the `.env` file.

5. To stop the container:

```bash
docker compose down
```

## Access

The database is reachable from:

- `localhost:<POSTGRES_HOST_PORT>` on the local machine
- `postgres:5432` from other containers in the Docker network `postgres-network`

## Volume

The `pgdata` volume persists the database, so data is not lost when stopped.

To stop and delete the volume (**this will erase ALL database data**):

```bash
docker compose down -v
```

## Port Configuration

The current port binding restricts access to the local machine.

To allow other machines on the network to connect, change it to:

```yaml
ports:
  - "${POSTGRES_HOST_PORT}:5432"
```

⚠️ **Note (Linux users):** Doing this bypasses UFW rules — see [Docker and UFW](https://docs.docker.com/engine/network/packet-filtering-firewalls/#docker-and-ufw).