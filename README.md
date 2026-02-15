# DraftBridge

AI-powered architectural co-pilot that transforms hand-drawn sketches into professional 3D visualizations and CAD/BIM files.

## Architecture

DraftBridge employs a microservices architecture built on AWS, leveraging Amazon Nova for image generation, Amazon Bedrock for intelligent analysis, and specialized processing pipelines for sketch interpretation and professional file export.

### Services

- **API Gateway** (Port 3000): Main entry point and request routing
- **Sketch Processor** (Port 3003): Analyzes and interprets hand-drawn sketches
- **Intelligence Agent** (Port 3001): Provides architectural analysis and compliance checking
- **Export System** (Port 3002): Converts designs to professional CAD/BIM formats

### Infrastructure

- **AWS CDK**: Infrastructure as Code for all AWS resources
- **DynamoDB**: NoSQL database for storing sketches, designs, and metadata
- **S3**: Object storage for images, renders, and exported files
- **CloudFront**: CDN for fast content delivery
- **ECS Fargate**: Containerized microservices deployment
- **CloudWatch**: Monitoring, logging, and alerting

## Quick Start

### Prerequisites

- Node.js 18+
- Docker and Docker Compose
- AWS CLI configured (for deployment)
- AWS CDK CLI installed

### Local Development

1. **Install dependencies:**
   ```bash
   npm install
   ```

2. **Build all services:**
   ```bash
   npm run build
   ```

3. **Start services with Docker Compose:**
   ```bash
   npm run dev
   ```

4. **View logs:**
   ```bash
   npm run dev:logs
   ```

5. **Stop services:**
   ```bash
   npm run dev:down
   ```

### Testing

```bash
# Run all tests
npm test

# Run tests for specific service
npm run test:api-gateway
npm run test:sketch-processor-ts
npm run test:intelligence-agent
npm run test:export-system
```

### Deployment

1. **Bootstrap CDK (first time only):**
   ```bash
   cd infrastructure/cdk
   npm run bootstrap
   ```

2. **Deploy to development:**
   ```bash
   npm run deploy:dev
   ```

3. **Deploy to production:**
   ```bash
   npm run deploy:prod
   ```

## Project Structure

```
DraftBridge/
├── services/                    # Microservices
│   ├── api-gateway/            # Main API Gateway service
│   ├── sketch-processor-ts/    # Sketch analysis service
│   ├── intelligence-agent/     # AI analysis and compliance
│   └── export-system/          # CAD/BIM export service
├── shared/                     # Shared libraries and models
│   ├── src/
│   │   ├── models/            # TypeScript interfaces and schemas
│   │   ├── config/            # Configuration management
│   │   └── utils/             # Utility functions
├── infrastructure/             # Infrastructure as Code
│   └── cdk/                   # AWS CDK stacks
│       ├── src/stacks/        # CDK stack definitions
│       └── cdk.json           # CDK configuration
├── frontend/                   # Web frontend (future)
├── docs/                      # Documentation
└── scripts/                   # Build and deployment scripts
```

## Development Workflow

1. **Feature Development**: Work in feature branches
2. **Testing**: All services must have unit and integration tests
3. **Code Quality**: ESLint and Prettier for consistent code style
4. **Type Safety**: Full TypeScript coverage with strict mode
5. **Infrastructure**: All AWS resources defined in CDK
6. **Monitoring**: Comprehensive logging and metrics collection

## Environment Variables

### Common Variables
- `NODE_ENV`: Environment (development, staging, production)
- `AWS_REGION`: AWS region for services
- `LOG_LEVEL`: Logging level (debug, info, warn, error)

### Service-Specific Variables
- `DYNAMODB_TABLE_PREFIX`: Prefix for DynamoDB table names
- `S3_BUCKET_NAME`: S3 bucket for assets
- `CLOUDFRONT_DOMAIN`: CloudFront distribution domain

## API Documentation

### Health Checks
- `GET /health` - Service health status

### API Gateway Endpoints
- `GET /v1/sketches` - List sketches
- `POST /v1/sketches` - Upload new sketch
- `GET /v1/designs` - List designs
- `POST /v1/designs` - Create new design
- `GET /v1/renders` - List renders
- `GET /v1/exports` - List exported files

## Monitoring and Logging

### CloudWatch Dashboards
- Performance metrics for all services
- Error rates and critical alerts
- Business metrics (uploads, renders, exports)

### Alarms
- Sketch processing > 30 seconds
- Render generation > 2 minutes
- Video generation > 5 minutes
- High error rates
- Critical system errors

### Log Groups
- `/draftbridge/{environment}/application` - Application logs
- `/draftbridge/{environment}/performance` - Performance metrics
- `/draftbridge/{environment}/security` - Security events

## Performance Requirements

Based on the design document requirements:

- **Sketch Processing**: ≤ 30 seconds (Requirements 10.1)
- **4K Render Generation**: ≤ 2 minutes (Requirements 10.2)
- **Video Generation**: ≤ 5 minutes (Requirements 10.3)
- **Concurrent Users**: Maintain performance standards (Requirements 10.4)
- **Load Management**: Queue requests with estimated completion times (Requirements 10.5)

## Security

- **Authentication**: JWT-based authentication
- **Authorization**: Role-based access control
- **Data Encryption**: At rest and in transit
- **Network Security**: VPC with private subnets
- **API Security**: Rate limiting and input validation
- **Container Security**: Non-root users and minimal images

## Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Add tests for new functionality
5. Ensure all tests pass
6. Submit a pull request

## License

MIT License - see LICENSE file for details