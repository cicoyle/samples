# Inventory Service (Java)

This is the Java Inventory Service that handles inventory reservation as an activity in the multi-app e-commerce scenario.

## Overview

The Inventory Service is responsible for:
- Checking inventory availability for requested items
- Reserving inventory items for orders
- Updating inventory counts after reservation
- Managing inventory data and stock levels

## Architecture

This Java service acts as an activity that is called by the Go Order Orchestrator. It demonstrates:
- **Activity Implementation**: Single-purpose inventory management
- **Data Validation**: Comprehensive inventory availability checks
- **Transaction Management**: Atomic inventory reservation operations
- **Error Handling**: Graceful handling of inventory shortages

## Activity Steps

1. **Check Inventory Availability**: Validates that all requested items are in stock
2. **Reserve Inventory Items**: Reserves the requested quantities
3. **Update Inventory Counts**: Updates the database with new stock levels

## Running the Service

1. Make sure you have Java 17+ and Maven installed

2. Build the project:
   ```bash
   mvn clean package
   ```

3. Run with Dapr:
   ```bash
   dapr run --app-id inventory-service --app-port 50003 --dapr-http-port 3503 --dapr-grpc-port 50003 -- java -jar target/inventory-service-1.0.0.jar
   ```

4. The service will start on port 50003 and register the `ReserveInventoryActivity`

## Configuration

The service uses Redis as the state store for workflow persistence. Make sure Redis is running on `localhost:6379`.

## Inventory Management

The service simulates inventory management with:
- **Availability Checks**: Validates stock levels before reservation
- **Atomic Reservations**: Ensures all items are reserved or none are
- **Stock Updates**: Maintains accurate inventory counts
- **Error Recovery**: Handles partial failures gracefully

## Error Handling

The service includes comprehensive error handling:
- Inventory shortage scenarios
- Reservation failures
- Database connection issues
- Timeout and retry logic
- Graceful degradation for non-critical failures
