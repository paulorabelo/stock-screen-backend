# Stock Screen Backend

Java-based backend for a stock screening application, providing APIs to fetch, filter, and analyze stock data.

## Structure

- Standard Maven project layout:
  - `src/main/java`: Production source code
  - `src/main/resources`: Configuration files (e.g., application.properties)
  - `src/test/java`: Unit tests
- Includes `mvnw` and `mvnw.cmd` (Maven Wrapper) for building without requiring Maven installed globally.
- `pom.xml` defines dependencies and build configuration.

## Getting Started

### Prerequisites

- Java JDK (version 11 or later recommended)
- Maven (or use the provided Maven Wrapper)

### Building and Running



Alternatively, after building, run the generated JAR:



## API Endpoints

(To be documented based on actual implementation. Common endpoints may include:)
- `GET /stocks` - List all stocks
- `GET /stocks/{symbol}` - Get details for a specific stock
- `POST /stocks/screen` - Filter stocks based on criteria
- `GET /stocks/indicators/{symbol}` - Get technical indicators

## Technologies

- Java
- Maven
- Possibly Spring Boot (if used)
- RESTful API design

## Notes

This backend is likely paired with a frontend application (see related repository `project-stock-screen` for a potential full-stack version).

