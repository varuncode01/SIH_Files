# Deployment Guide - Smart Crop Advisory Platform

## SIH 2025 Production Deployment

### Quick Deployment (Recommended)

```bash
# Clone repository
git clone <repository-url>
cd smart-crop-advisory

# Run setup script
chmod +x setup.sh
./setup.sh

# Access application
open http://localhost:3000
```

### Manual Deployment

#### Prerequisites
- Docker 20.10+
- Docker Compose 1.29+
- 4GB RAM minimum
- 10GB free disk space

#### Step 1: Environment Configuration
```bash
cp .env.example .env
# Edit .env with production values
```

#### Step 2: Build and Deploy
```bash
docker-compose -f deployment/docker-compose.yml up --build -d
```

#### Step 3: Verify Deployment
```bash
# Check service status
docker-compose -f deployment/docker-compose.yml ps

# Check logs
docker-compose -f deployment/docker-compose.yml logs -f
```

### Production Considerations

#### Security
- Change default passwords in .env
- Configure SSL certificates
- Set up proper firewall rules
- Enable authentication and authorization

#### Scaling
- Use Docker Swarm or Kubernetes for multi-server deployment
- Configure load balancers (Nginx/HAProxy)
- Set up database replication
- Implement caching layers

#### Monitoring
- Set up application monitoring (Prometheus/Grafana)
- Configure log aggregation (ELK Stack)
- Set up alerts for critical metrics
- Monitor resource usage

#### Backup Strategy
- Database backups (automated daily)
- Image storage backups
- ML model version control
- Configuration backups

### Cloud Deployment Options

#### AWS Deployment
```bash
# Use ECS with Fargate
# RDS for PostgreSQL
# ElastiCache for Redis
# S3 for file storage
# CloudFront for CDN
```

#### GCP Deployment
```bash
# Use Cloud Run for containers
# Cloud SQL for PostgreSQL
# Memorystore for Redis
# Cloud Storage for files
# Cloud CDN for content delivery
```

#### Azure Deployment
```bash
# Use Container Instances
# Azure Database for PostgreSQL
# Azure Cache for Redis
# Blob Storage for files
# Azure CDN
```

### Performance Optimization

#### Database Optimization
- Index frequently queried columns
- Use connection pooling
- Implement read replicas
- Regular VACUUM and ANALYZE

#### API Performance
- Enable response caching
- Use async processing for heavy tasks
- Implement request rate limiting
- Optimize database queries

#### Frontend Optimization
- Enable PWA caching
- Optimize images and assets
- Use CDN for static files
- Implement lazy loading

### SIH 2025 Demo Setup

For live demonstration:
1. Ensure stable internet connection
2. Test image upload functionality
3. Prepare sample crop images
4. Test offline capabilities
5. Prepare backup demo environment

### Troubleshooting

#### Common Issues
```bash
# Service won't start
docker-compose -f deployment/docker-compose.yml logs [service_name]

# Database connection issues
docker exec -it crop-advisory-db psql -U crop_user -d crop_advisory

# Redis connection issues  
docker exec -it crop-advisory-redis redis-cli

# ML model loading issues
docker exec -it crop-advisory-backend python -c "from app.ml.disease_detector import DiseaseDetectionService; print('ML OK')"
```

#### Performance Issues
- Check resource usage: `docker stats`
- Monitor logs for errors
- Verify database performance
- Check network connectivity

#### Recovery Procedures
- Database recovery from backup
- Service restart procedures
- Data integrity checks
- Rollback strategies
