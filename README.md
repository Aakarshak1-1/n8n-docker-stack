<<<<<<< HEAD
# n8n Local Development Setup

This repository contains the configuration for running n8n locally for development and testing purposes, with easy migration path to AWS.

## Table of Contents
- [Local Setup](#local-setup)
- [Environment Variables](#environment-variables)
- [Advanced Features](#advanced-features)
- [Monitoring and Health Checks](#monitoring-and-health-checks)
- [Email Configuration](#email-configuration)
- [Redis Integration](#redis-integration)
- [Database Configuration](#database-configuration)
- [Resource Management](#resource-management)
- [Migration to AWS](#migration-to-aws)
- [Troubleshooting](#troubleshooting)

## Local Setup

1. Install Docker and Docker Compose if you haven't already
2. Clone this repository
3. Create a `.env` file with your configuration (optional, defaults are provided)
4. Create required directories:
   ```bash
   mkdir -p n8n-custom postgres-init
   ```
5. Run the following command to start the services:
   ```bash
   docker-compose up -d
   ```
6. Access n8n at http://localhost:5678

## Environment Variables

The setup uses environment variables for configuration. Create a `.env` file based on `.env.example`:

### Core Configuration
```
N8N_HOST=localhost
N8N_PORT=5678
N8N_PROTOCOL=http
N8N_USER_MANAGEMENT_DISABLED=false
N8N_BASIC_AUTH_ACTIVE=true
N8N_BASIC_AUTH_USER=admin
N8N_BASIC_AUTH_PASSWORD=your-secure-password
N8N_ENCRYPTION_KEY=your-encryption-key
```

### Additional Settings
```
N8N_EDITOR_BASE_URL=http://localhost:5678
N8N_METRICS=true
N8N_DIAGNOSTICS_ENABLED=true
N8N_PUBLIC_API_DISABLED=true
N8N_LOG_LEVEL=info
N8N_LOG_OUTPUT=console
N8N_TIMEZONE=UTC
```

### Email Configuration
```
N8N_EMAIL_MODE=smtp
N8N_SMTP_HOST=smtp.gmail.com
N8N_SMTP_PORT=587
N8N_SMTP_USER=your-email@gmail.com
N8N_SMTP_PASS=your-app-password
N8N_SMTP_SENDER=n8n@yourdomain.com
```

### Database Configuration
```
DB_TYPE=postgresdb
DB_POSTGRESDB_HOST=postgres
DB_POSTGRESDB_PORT=5432
DB_POSTGRESDB_DATABASE=n8n
DB_POSTGRESDB_USER=n8n
DB_POSTGRESDB_PASSWORD=your-db-password
```

### Redis Configuration (Optional)
```
REDIS_HOST=redis
REDIS_PORT=6379
REDIS_PASSWORD=your-redis-password
```

## Advanced Features

### Monitoring and Health Checks

The setup includes comprehensive health checks and monitoring:

1. **n8n Health Check**
   - Checks the `/healthz` endpoint every 30 seconds
   - Retries 3 times before marking as unhealthy
   - Timeout of 10 seconds per check

2. **PostgreSQL Health Check**
   - Uses `pg_isready` to verify database connectivity
   - Checks every 10 seconds
   - 5 retries before marking as unhealthy

3. **Redis Health Check** (if enabled)
   - Uses `redis-cli ping` to verify Redis connectivity
   - Checks every 10 seconds
   - 5 retries before marking as unhealthy

4. **Metrics and Diagnostics**
   - Enabled by default (`N8N_METRICS=true`)
   - Provides performance metrics
   - Helps in troubleshooting and optimization

### Email Configuration

Email notifications are configured using SMTP:

1. **SMTP Settings**
   - Default configuration for Gmail SMTP
   - Supports TLS encryption
   - Customizable sender address

2. **Usage**
   - Used for workflow notifications
   - Error reporting
   - User notifications

### Redis Integration

Redis is included as an optional component for queue management:

1. **Features**
   - Persistent storage with `appendonly yes`
   - Health monitoring
   - Resource limits

2. **Usage**
   - Queue management for workflows
   - Caching
   - Rate limiting

3. **Configuration**
   - Enable in n8n settings
   - Configure connection in workflows
   - Set up proper authentication

### Database Configuration

PostgreSQL is configured with enhanced security and performance:

1. **Security Features**
   - Data checksums enabled
   - Custom initialization scripts support
   - Resource limits and reservations

2. **Persistence**
   - Data volume for persistence
   - Regular health checks
   - Automatic restarts

### Resource Management

Each service has defined resource limits:

1. **n8n**
   - CPU: 0.5-1 core
   - Memory: 1-2GB
   - Automatic restarts

2. **PostgreSQL**
   - CPU: 0.5-1 core
   - Memory: 1-2GB
   - Data volume persistence

3. **Redis** (if enabled)
   - CPU: 0.2-0.5 core
   - Memory: 256-512MB
   - Persistent storage

## Migration to AWS

### Preparation Steps

1. **Backup Your Data**
   - Export your workflows from n8n UI
   - Backup your PostgreSQL database
   - Save your credentials and environment variables

2. **AWS Infrastructure Setup**
   - Create an RDS PostgreSQL instance
   - Set up an ECS cluster or EC2 instance
   - Configure security groups and VPC
   - Set up a load balancer if needed

### Migration Process

1. **Database Migration**
   - Use AWS Database Migration Service (DMS) or pg_dump/pg_restore
   - Ensure the database schema matches your local setup

2. **Application Migration**
   - Update the Docker Compose configuration for AWS
   - Modify environment variables for AWS services
   - Set up proper IAM roles and permissions

3. **Data Migration**
   - Import your workflows into the new instance
   - Update credentials and connections
   - Test all workflows thoroughly

### AWS Deployment Options

1. **ECS (Recommended)**
   - Convert the Docker Compose file to ECS task definition
   - Use Fargate for serverless container management
   - Set up auto-scaling and monitoring

2. **EC2**
   - Deploy Docker containers directly on EC2
   - Use ECS or Kubernetes for orchestration
   - Set up proper monitoring and logging

## Best Practices

1. **Security**
   - Use AWS Secrets Manager for sensitive data
   - Implement proper IAM roles and policies
   - Enable encryption at rest and in transit
   - Regularly rotate encryption keys and passwords

2. **Backup and Recovery**
   - Set up automated backups for RDS
   - Implement disaster recovery procedures
   - Regular testing of backup restoration
   - Maintain backup schedules

3. **Monitoring**
   - Use CloudWatch for monitoring
   - Set up alerts for critical metrics
   - Implement proper logging
   - Monitor resource utilization

## Troubleshooting

Common issues and solutions:

1. **Database Connection Problems**
   - Check security groups and VPC settings
   - Verify database credentials
   - Check network connectivity
   - Review database logs

2. **Workflow Execution Errors**
   - Verify credentials and permissions
   - Check workflow logs
   - Review error messages
   - Test individual nodes

3. **Performance Issues**
   - Monitor resource utilization
   - Check for bottlenecks
   - Review workflow optimization
   - Scale resources as needed

4. **Email Configuration Issues**
   - Verify SMTP settings
   - Check email provider requirements
   - Review authentication settings
   - Test email sending

5. **Redis Connection Problems**
   - Verify Redis configuration
   - Check network connectivity
   - Review authentication settings
   - Monitor Redis logs 
=======
# n8n-docker-stack
>>>>>>> 7b47f76f8b0bb7cdd816a47fa235aa3cd9305f37
