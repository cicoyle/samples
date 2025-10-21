# AI Recommendation Service (Java)

This is the Java AI Recommendation Service that generates personalized product recommendations as an activity in the multi-app e-commerce scenario.

## Overview

The AI Recommendation Service is responsible for:
- Analyzing customer purchase history and behavior patterns
- Processing current order items to understand customer preferences
- Generating AI-powered personalized product recommendations
- Ranking and filtering recommendations for optimal relevance

## Architecture

This Java service acts as an activity that is called by the Go Order Orchestrator. It demonstrates:
- **AI Integration**: Machine learning-powered recommendation generation
- **Data Analysis**: Customer profile and order analysis
- **Performance Optimization**: Efficient recommendation ranking and filtering
- **Scalability**: AI workloads that can be scaled independently

## AI Processing Steps

1. **Customer Profile Analysis**: Analyzes customer purchase history and preferences
2. **Order Analysis**: Processes current order items to understand context
3. **Recommendation Generation**: AI-powered product recommendation generation
4. **Ranking and Filtering**: Optimizes recommendations for relevance and performance

## Running the Service

1. Make sure you have Java 17+ and Maven installed

2. Build the project:
   ```bash
   mvn clean package
   ```

3. Run with Dapr:
   ```bash
   dapr run --app-id ai-recommendation-service --app-port 50004 --dapr-http-port 3504 --dapr-grpc-port 50004 -- java -jar target/ai-recommendation-service-1.0.0.jar
   ```

4. The service will start on port 50004 and register the `GeneratePersonalizedRecommendationsActivity`

## Configuration

The service uses Redis as the state store for workflow persistence. Make sure Redis is running on `localhost:6379`.

## AI Features

The service simulates advanced AI capabilities:
- **Customer Profiling**: Analyzes purchase history and behavior patterns
- **Contextual Analysis**: Understands current order context
- **Recommendation Engine**: Generates personalized product suggestions
- **Intelligent Ranking**: Optimizes recommendations for relevance

## Performance Characteristics

- **Processing Time**: Simulates realistic AI processing delays (3-4 seconds)
- **Scalability**: Designed to handle high-volume recommendation requests
- **Resource Usage**: Optimized for AI workloads with dedicated resources
- **Caching**: Simulates intelligent caching for improved performance

## Error Handling

The service includes comprehensive error handling:
- AI model failures and fallbacks
- Data processing errors
- Timeout and retry logic
- Graceful degradation for non-critical failures
