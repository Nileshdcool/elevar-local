# Elevar Local

Elevar Local is a local development environment designed to simplify working with MongoDB, PostgreSQL databases, and a local npm registry using Verdaccio. It leverages Docker Compose to provide a seamless setup for these services.

## Project Structure

```
elevar-local/
├── .gitignore          # Git ignore rules
├── docker-compose.yml  # Docker Compose configuration
├── README.md           # Project documentation
├── mongodb_data/       # MongoDB data directory (ignored in version control)
├── mongodb_init/       # MongoDB initialization scripts (ignored in version control)
├── postgres_data/      # PostgreSQL data directory (ignored in version control)
├── verdaccio_data/     # Verdaccio data directory (ignored in version control)
```

## Prerequisites

- [Docker](https://www.docker.com/) and [Docker Compose](https://docs.docker.com/compose/) installed on your system.
- Basic understanding of MongoDB, PostgreSQL, and npm registry concepts.

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

3. Access the services:
    - **MongoDB**: Connect to `localhost:27018`.
    - **PostgreSQL**: Connect to `localhost:5433`.
    - **Verdaccio**: Access the local npm registry at `http://localhost:4873`.

## Configuration

### MongoDB
- MongoDB data is stored in the `mongodb_data/` directory.
- Initialization scripts can be added to the `mongodb_init/` directory for setting up collections or seeding data.

### PostgreSQL
- PostgreSQL data is stored in the `postgres_data/` directory.
- Configuration files can be customized as needed.

### Verdaccio
- Verdaccio data is stored in the `verdaccio_data/` directory.
- Use the Verdaccio web interface at `http://localhost:4873` to manage your local npm packages.
- To publish a package to Verdaccio, configure your npm client:
    ```bash
    npm set registry http://localhost:4873
    ```
- Authenticate with Verdaccio (if authentication is enabled):
    ```bash
    npm adduser --registry http://localhost:4873
    ```

#### Configuring Verdaccio
- The Verdaccio configuration file is located at `verdaccio_data/config.yaml`.
- You can customize the configuration to enable authentication, set storage paths, or define access permissions.
- After making changes to `config.yaml`, restart the Verdaccio service:
    ```bash
    docker-compose restart verdaccio
    ```
- For more details on configuration options, refer to the [Verdaccio configuration documentation](https://verdaccio.org/docs/configuration).
    ```

## Ignored Files and Directories

The following directories are ignored in version control as specified in the `.gitignore` file:
- `mongodb_data/`
- `mongodb_init/`
- `postgres_data/`
- `verdaccio_data/`

This ensures that sensitive or large data files are not accidentally committed to the repository.

## Troubleshooting

- Ensure Docker is running and has sufficient resources allocated.
- Use `docker-compose logs` to view logs for MongoDB, PostgreSQL, and Verdaccio services.
- For Verdaccio-specific issues, refer to the [Verdaccio documentation](https://verdaccio.org/docs).

## Contributing

Contributions are welcome! Please fork the repository, create a feature branch, and submit a pull request.

## License

This project is licensed under the MIT License. See the `LICENSE` file for details.
