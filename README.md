# ELK Stack Project (Elasticsearch, Logstash, Kibana)

> Also available in: [Español](README.es.md)

This project implements a full ELK stack using Docker Compose, configured for data processing and visualization. The stack includes Elasticsearch, Logstash, Kibana, Filebeat, and Metricbeat to provide a complete monitoring and data analysis solution.

## Features

- **Elasticsearch 8.15.2**: Distributed database for search and analytics.
- **Logstash**: Data processing pipeline.
- **Kibana**: Data visualization and exploration interface.
- **Filebeat**: Log data collection and shipping.
- **Metricbeat**: System and service metrics monitoring.
- **Security**: TLS/SSL authentication with auto-generated certificates.

## Prerequisites

- Docker and Docker Compose
- At least 8GB of available RAM (recommended)
- Available ports: 9204 (Elasticsearch) and 5604 (Kibana)

## Project Structure

```
.
├── .env                      # Environment variables and configuration
├── docker-compose.yml        # Docker services configuration
├── logstash.conf             # Main Logstash configuration
├── filebeat.yml              # Filebeat configuration
├── metricbeat.yml            # Metricbeat configuration
├── datos_logstash/           # Additional Logstash configurations
│   ├── log_filter.conf       # Log processing filters
│   ├── log_input.conf        # Data input configuration
│   └── log_output.conf       # Data output configuration
└── logstash_ingest_data/     # Data ingestion directory
    └── logs.log              # Log file for processing
```

## Configuration

> [!NOTE]
> Rename and modify the `.env.example` file to `.env`

The project uses environment variables defined in the `.env` file:

- `ELASTIC_PASSWORD`: Password for the elastic user
- `KIBANA_PASSWORD`: Password for the kibana_system user
- `STACK_VERSION`: ELK stack version (currently 8.15.2)
- `CLUSTER_NAME`: Elasticsearch cluster name
- `ES_PORT`: Elasticsearch port (9204)
- `KIBANA_PORT`: Kibana port (5604)
- `ES_MEM_LIMIT`, `KB_MEM_LIMIT`, `LS_MEM_LIMIT`: Memory limits for services

## Starting the Stack

```bash
# Clone the repository
git clone https://github.com/JonAlvz/ELK.git
cd ELK

# Start the services
docker-compose up -d
```

## Accessing the Services

Once the services are running:

- **Kibana**: https://localhost:5604
  - Username: elastic
  - Password: admin123 (or as configured in .env)

- **Elasticsearch**: https://localhost:9204
  - Username: elastic
  - Password: admin123 (or as configured in .env)

## Data Processing

The project is configured to process two types of data:

1. **F1 Data**: Formula 1 race and event information.
2. **RTVE Data**: News and multimedia content.

Data is processed through Logstash and stored in Elasticsearch for later analysis in Kibana.

## Specific Features

- **Data transformation**: Advanced Logstash processing to structure complex data
- **Docker monitoring**: Metricbeat is configured to collect Docker container metrics
- **Built-in security**: Automatically generated SSL/TLS certificates

## Troubleshooting

- If services do not start correctly, check the logs with `docker-compose logs -f`
- Make sure you have enough memory available to run the full stack
- Verify that the configured ports (9204, 5604) are not being used by other applications

## License

This project uses the Elastic Stack basic license.
