# Order Orchestrator (Go)

This is the main orchestrator service for the e-commerce order processing workflow. It coordinates the entire order lifecycle across multiple services.

## Overview

The Order Orchestrator is responsible for:
- Validating incoming orders
- Coordinating payment processing with the Java Payment Service
- Managing inventory reservations with the Java Inventory Service
- Generating AI-powered recommendations with the Java AI Service
- Finalizing order completion

## Architecture

This Go service acts as the main workflow orchestrator and calls:
- **Java Payment Service**: Child workflow for complex payment processing
- **Java Inventory Service**: Activity for inventory reservation
- **Java AI Service**: Activity for personalized recommendations

## Running the Service

1. Make sure you have the required dependencies:
   ```bash
   go mod tidy
   ```

2. Run with Dapr:
   ```bash
   dapr run --app-id order-orchestrator --app-port 50001 --dapr-http-port 3501 --dapr-grpc-port 50001 -- go run .
   ```

3. The service will start on port 50001 and register the `OrderProcessingWorkflow`

## API Endpoints

- **Workflow Start**: `/OrderProcessingWorkflow/start`
- **Workflow Invocation**: `/OrderProcessingWorkflow/invoke`

## Workflow Steps

1. **ValidateOrder**: Validates the incoming order data
2. **ProcessPayment**: Calls Java Payment Service child workflow
3. **ReserveInventory**: Calls Java Inventory Service activity
4. **GenerateRecommendations**: Calls Java AI Service activity
5. **CompleteOrder**: Finalizes the order processing

## Configuration

The service uses Redis as the state store for workflow persistence. Make sure Redis is running on `localhost:6379`.
