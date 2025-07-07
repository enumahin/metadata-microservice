# CDR Metadata Service

A microservice responsible for managing metadata in the CDR (Call Detail Records) system. This service handles the storage, retrieval, and management of metadata associated with call records.

## Features

- CRUD operations for metadata entities
- Integration with MySQL database
- Event-driven architecture with RabbitMQ
- Circuit breaking with Resilience4j
- Health monitoring and metrics
- API documentation with Swagger/OpenAPI

## Prerequisites

- Java 17 or higher
- Maven 3.6.3 or higher
- MySQL 8.0 or higher
- RabbitMQ 3.8 or higher
- Eureka Discovery Server (running on port 8761 by default)
- Spring Cloud Config Server (running on port 8071 by default, optional)

## Environment Variables

### Required Configuration

```properties
# Server Configuration
SERVER_PORT=8010

# Spring Application Name
SPRING_APPLICATION_NAME=metadata

# Database Configuration
SPRING_DATASOURCE_URL=jdbc:mysql://localhost:3306/metadata?createDatabaseIfNotExist=true
SPRING_DATASOURCE_USERNAME=root
SPRING_DATASOURCE_PASSWORD=root

# JPA/Hibernate Configuration
SPRING_JPA_HIBERNATE_DDL_AUTO=update
SPRING_JPA_DATABASE_PLATFORM=org.hibernate.dialect.MySQL8Dialect

# Eureka Client Configuration
EUREKA_CLIENT_SERVICE_URL_DEFAULTZONE=http://localhost:8761/eureka/

# RabbitMQ Configuration
SPRING_RABBITMQ_HOST=localhost
SPRING_RABBITMQ_PORT=5672
SPRING_RABBITMQ_USERNAME=guest
SPRING_RABBITMQ_PASSWORD=guest
```

### Optional Configuration

```properties
# JPA/Hibernate
SPRING_JPA_SHOW_SQL=true
SPRING_JPA_PROPERTIES_HIBERNATE_FORMAT_SQL=true

# Actuator Endpoints
MANAGEMENT_ENDPOINTS_WEB_EXPOSURE_INCLUDE=health,info,metrics
MANAGEMENT_ENDPOINT_HEALTH_SHOW_DETAILS=always

# Circuit Breaker
RESILIENCE4J_CIRCUITBREAKER_INSTANCES_DEFAULT_REGISTER_HEALTH_INDICATOR=true
RESILIENCE4J_CIRCUITBREAKER_INSTANCES_DEFAULT_SLIDING_WINDOW_SIZE=10
```

## API Endpoints

### Metadata Management

- `GET /api/v1/metadata` - Get all metadata
- `GET /api/v1/metadata/{id}` - Get metadata by ID
- `POST /api/v1/metadata` - Create new metadata
- `PUT /api/v1/metadata/{id}` - Update existing metadata
- `DELETE /api/v1/metadata/{id}` - Delete metadata

### Health and Monitoring

- `GET /actuator/health` - Application health status
- `GET /actuator/info` - Application information
- `GET /actuator/metrics` - Application metrics

## Getting Started

1. **Set up the database**
   ```sql
   CREATE DATABASE IF NOT EXISTS metadata;
   ```

2. **Build the application**
   ```bash
   mvn clean install
   ```

3. **Run the application**
   ```bash
   java -jar target/metadata-1.0.0.jar
   ```
   Or using Maven:
   ```bash
   mvn spring-boot:run
   ```

4. **Access the API documentation**
   ```
   http://localhost:8010/swagger-ui.html
   ```

## Database Schema

The service uses the following main entities:

- **Metadata**: Stores metadata information

## Event Handling

The service publishes and subscribes to the following events:

- **Published Events**:
  - `MetadataCreatedEvent`
  - `MetadataUpdatedEvent`
  - `MetadataDeletedEvent`

- **Subscribed Events**:
  - `SomeExternalEvent` (example)

## Monitoring

The service exposes the following monitoring endpoints:

- Health: `GET /actuator/health`
- Info: `GET /actuator/info`
- Metrics: `GET /actuator/metrics`
- Prometheus: `GET /actuator/prometheus`

## Dependencies

- Spring Boot Web
- Spring Data JPA
- Spring Cloud OpenFeign
- Spring Cloud Circuit Breaker
- Spring Boot Actuator
- Spring Cloud Config Client
- Spring Cloud Netflix Eureka Client
- Spring AMQP (RabbitMQ)
- MySQL Connector/J
- Lombok
- MapStruct

## License

[Specify your license here]

## Contact

[Your contact information]
