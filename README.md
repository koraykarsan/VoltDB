# VoltDB Docker Setup

This project provides a Docker configuration to run VoltDB, an in-memory SQL database that emphasizes high-speed, high-volume operational workloads. It is designed to be run on Docker, allowing for easy setup and scalability in development, testing, and production environments.

## Prerequisites

Before you begin, ensure you have the following installed on your system:

- Docker Engine
  - Installation guides can be found [here](https://docs.docker.com/engine/install/).
- Docker Compose (optional for managing multi-container setups)
  - Installation guides are available [here](https://docs.docker.com/compose/install/).

## SQL Commands

-- Create a table
CREATE TABLE mth3902 (
    id BIGINT NOT NULL,
    start_date_epoch BIGINT,
    create_user VARCHAR(32),
    CONSTRAINT mth3902_pk PRIMARY KEY (id)
);

-- Partition the table on 'id' column
PARTITION TABLE mth3902 ON COLUMN id;

-- Insert data into the table
INSERT INTO mth3902 (id, start_date_epoch, create_user) VALUES (1, 1698295044, 'MENNAN');
INSERT INTO mth3902 (id, start_date_epoch, create_user) VALUES (2, 1698295088, 'ERKUT');

-- Select data from the table
SELECT * FROM mth3902 LIMIT 1;

-- Create a stored procedure
CREATE PROCEDURE proc_select_mth3902_by_id
    PARTITION ON TABLE mth3902 COLUMN id
    AS 
    BEGIN
        SELECT start_date_epoch, create_user FROM mth3902 WHERE id = ?;
    END;

-- Execute the stored procedure
EXEC proc_select_mth3902_by_id 1;


<img width="1221" alt="Screenshot 2024-05-02 at 17 08 27" src="https://github.com/koraykarsan/voltdb/assets/108725475/58d0755c-ddc4-48e3-ac1e-ea805e9a3127">




