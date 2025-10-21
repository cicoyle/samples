# Payment Service (Java)

This is the Java Payment Service that handles complex payment processing as a child workflow in the multi-app e-commerce scenario.

## Overview

The Payment Service is responsible for:
- Validating payment methods
- Processing payment authorization
- Running AI-powered fraud detection for high-value transactions
- Finalizing payments and generating transaction IDs

## Architecture

This Java service acts as a child workflow that is called by the Go Order Orchestrator. It demonstrates:
- **Child Workflow**: Complex multi-step payment processing
- **AI Integration**: Fraud detection for transactions over $1000
- **Activity Chaining**: Multiple activities working together
- **Error Handling**: Comprehensive error handling and rollback scenarios

## Workflow Steps

1. **ValidatePaymentMethod**: Validates the payment method and amount
2. **ProcessPaymentAuthorization**: Processes payment authorization with the bank
3. **AIFraudDetection**: AI-powered fraud detection for high-value transactions (>$1000)
4. **FinalizePayment**: Finalizes the payment and generates transaction ID

## Running the Service

1. Make sure you have Java 17+ and Maven installed

2. Build the project:
   ```bash
   mvn clean package
   ```

3. Run with Dapr:
   ```bash
   dapr run --app-id payment-service --app-port 50002 --dapr-http-port 3502 --dapr-grpc-port 50002 -- java -jar target/payment-service-1.0.0.jar
   ```

4. The service will start on port 50002 and register the `PaymentProcessingWorkflow`

## Configuration

The service uses Redis as the state store for workflow persistence. Make sure Redis is running on `localhost:6379`.

## AI Fraud Detection

For transactions over $1000, the service automatically calls the AI fraud detection activity which:
- Analyzes transaction patterns
- Generates a fraud risk score
- Approves or rejects based on AI analysis
- Provides detailed reasoning for decisions

## Error Handling

The service includes comprehensive error handling:
- Payment method validation failures
- Authorization failures
- Fraud detection failures
- Network timeouts and retries
- Graceful degradation for non-critical failures
