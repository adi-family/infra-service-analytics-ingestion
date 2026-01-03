infra-service-analytics-ingestion, docker-compose, deployment, analytics

## Overview
- Docker Compose deployment for ADI Analytics Ingestion Service
- Receives analytics events from all services via HTTP
- Writes events to TimescaleDB for later querying
- License: BSL-1.0

## Structure
- `docker-compose.yml` - Deployment configuration
- Builds from `../../crates/adi-analytics-ingestion`

## Environment Variables
- `PORT` - Listen port (default: 8094)
- `DATABASE_URL` - PostgreSQL/TimescaleDB connection string
- `RUST_LOG` - Log level (info, debug, trace)

## API Endpoints
- `POST /events/batch` - Ingest batch of analytics events
- `GET /health` - Health check

## Deployment
```bash
docker compose up -d
```

## URL
Production: https://adi.the-ihor.com/api/analytics/ingest

## Notes
- Write-only service (no query endpoints)
- All services use lib-analytics-core to send events here
- Events are stored in TimescaleDB analytics_events hypertable
- Pairs with infra-service-analytics for querying metrics
