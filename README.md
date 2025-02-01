# Docker Development Environment

## Description
This project contains a `docker-compose.yml` configuration to run multiple database services and developer tools in Docker containers.

### Services:
- **CloudBeaver (DBeaver)** – Web-based database client
- **RedisInsight** – GUI for managing Redis
- **RabbitMQ** – Message broker with a management interface
- **MS SQL Server** – Microsoft SQL Server 2019 Express database server
- **PostgreSQL** – PostgreSQL database server
- **Redis** – NoSQL database server

---

## Requirements
- Docker
- Docker Compose

## Running the Services

Clone the repository and navigate to the project directory:
```sh
git clone https://github.com/git-df/docker-dev.git
cd docker-dev
```

To start the environment, run:
```sh
docker-compose up -d
```

To stop the containers:
```sh
docker-compose down
```

---

## Configuration Details

### CloudBeaver (DBeaver)
- **Ports:** 5550 → 8978
- **Access:** [http://localhost:5550](http://localhost:5550)
- **Persistent data:** `dbeaver_data:/opt/cloudbeaver/workspace`

### RedisInsight
- **Ports:** 5551 → 8001
- **Access:** [http://localhost:5551](http://localhost:5551)
- **Persistent data:** `redis_insight_data:/db`

### RabbitMQ
- **Ports:**
    - 5552 → 15672 (Management Panel)
    - 5553 → 5672 (AMQP Communication)
- **Access:** [http://localhost:5552](http://localhost:5552)
- **Default Password:** `Test123!`
- **Connection:**
    - `amqp://guest:Test123!@localhost:5553/`
- **Persistent data:** `rabbitmq_data:/var/lib/rabbitmq`

### MS SQL Server
- **Ports:** 5554 → 1433
- **Connection:**
    - `Data Source=127.0.0.1,5554;Database=Test;User Id=sa;Password=Test123!;TrustServerCertificate=True;`
- **Persistent data:** `mssql_data:/var/opt/mssql`

### PostgreSQL
- **Ports:** 5555 → 5432
- **Connection:**
    - `Server=127.0.0.1;Port=5555;Database=Test;User Id=postgres;Password=Test123!;`
- **Persistent data:** `postgres_data:/var/lib/postgresql/data`

### Redis
- **Ports:** 5556 → 6379
- **Password:** `Test123!`
- **Persistent data:** `redis_data:/data`

---

## Changing Configuration
If you want to modify the configuration, edit the `docker-compose.yml` file.

After making changes, restart the containers:
```sh
docker-compose down && docker-compose up -d
```

## Clearing Data
To remove all stored data in Docker volumes, run:
```sh
docker volume rm dbeaver_data redis_insight_data rabbitmq_data mssql_data postgres_data redis_data
```
**Warning:** Deleting volumes will permanently erase the stored data!