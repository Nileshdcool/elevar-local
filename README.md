# Elevar Local

Elevar Local is a local development environment designed to simplify working with MongoDB and PostgreSQL databases. It leverages Docker Compose to provide a seamless setup for local database services.

## Project Structure

```
elevar-local/
├── .gitignore          # Git ignore rules
├── docker-compose.yml  # Docker Compose configuration
├── README.md           # Project documentation
├── mongodb_data/       # MongoDB data directory (ignored in version control)
├── mongodb_init/       # MongoDB initialization scripts (ignored in version control)
├── postgres_data/      # PostgreSQL data directory (ignored in version control)
```

## Prerequisites

- [Docker](https://www.docker.com/) and [Docker Compose](https://docs.docker.com/compose/) installed on your system.
- Basic understanding of MongoDB and PostgreSQL.

## Getting Started

1. Clone the repository:
    ```bash
    git clone <repository-url>
    cd elevar-local
    ```

2. Start the services using Docker Compose:
    ```bash
    docker-compose up -d
    ```

3. Access the databases:
    - **MongoDB**: Connect to `localhost:27017`.
    - **PostgreSQL**: Connect to `localhost:5432`.

## Configuration

### MongoDB
- MongoDB data is stored in the `mongodb_data/` directory.
- Initialization scripts can be added to the `mongodb_init/` directory for setting up collections or seeding data.

### PostgreSQL
- PostgreSQL data is stored in the `postgres_data/` directory.
- Configuration files can be customized as needed.

## Ignored Files and Directories

The following directories are ignored in version control as specified in the `.gitignore` file:
- `mongodb_data/`
- `mongodb_init/`
- `postgres_data/`

This ensures that sensitive or large data files are not accidentally committed to the repository.

## Troubleshooting

- Ensure Docker is running and has sufficient resources allocated.
- Use `docker-compose logs` to view logs for MongoDB and PostgreSQL services.

## Contributing

Contributions are welcome! Please fork the repository, create a feature branch, and submit a pull request.

## License

This project is licensed under the MIT License. See the `LICENSE` file for details.
