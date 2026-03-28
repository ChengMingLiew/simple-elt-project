# Custom ElT Project

A simple project that demonstrates Extract, Transform and Load (ELT) process and utilizes Docker, PostgreSQL, Airflow and DBT.

## Repository Structure

1. docker-compose.yaml: This file containes the configuration for Docker Compose, which is used to orchestrate multiple Docker containers. It defines 3 servies:
   - `source_postgres`: The source PostgreSQL database.
   - `destination_potgres`: The destination PostgreSQL database.
   - `elt_script`: The service that runs the ELT script.
2. elt_scripit/Dockerfile: This Dockerfile sets up the Python environment and installs the PostgreSql client. It also copies the ELT script into the container and sets it as the default command.
3. elt_script/elt_script.py: This Python script performs the ELT process. It waits for the source PostgreSQL database to become available, then dumps its data to a SQL file and loads this data into the destination PostgreSQL database.
4. source_db_init/init.sql: This SQL script initializes the source database with sample data. It creates tables for users, films, film categories, actors, and film actors, and inserts sample data into these tables.

## How It Works

1. Docker Compose: Using the `docker-compose.yaml` file, three Docker containers are spun up:
   - A source PostgreSQL database with sample data.
   - A destination PostgreSQL database.
   - A Python environment that runs the ELT script.
2. ELT Process: The elt_script.py waits for the source PostgreSQL database to become available. Once it's available, the script uses pg_dump to dump the source database to a SQL file. Then, it uses psql to load this SQL file into the destination PostgreSQL database.
3. Database Initialization: The init.sql script initializes the source database with sample data. It creates several tables and populates them with sample data.

## Getting Started

1. Ensure that you have your Docker and Docker Compose installed on your machine
2. Clone this repository.
3. Navigate to the repository directory and run `docker compose build` to build the images of the services.
4. Run `docker compose up init-airfloww -d` and then `docker compose up`.
5. Once all the containers are up and running, the ELT process will start automatically.
6. After the ELT process completes, you can access the source and destination PostgreSQL databses on ports 5433 and 5434, respectively.
