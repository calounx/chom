# CHOM - Cloud Hosting & Observability Manager

A multi-tenant SaaS platform for WordPress hosting management with integrated observability.

## Overview

CHOM is a Laravel-based control plane that orchestrates VPS infrastructure and observability stack into a unified hosting platform. It provides:

- **Multi-tenant Architecture**: Organizations, tenants, and team management
- **Site Management**: WordPress, HTML, and Laravel site provisioning
- **VPS Fleet Management**: Automated server allocation and load balancing
- **Backup Management**: Automated backups with retention policies
- **Observability**: Integrated Prometheus metrics and Loki logs
- **Team Collaboration**: Role-based access control (Owner, Admin, Member, Viewer)

## Requirements

- PHP 8.2+
- SQLite / MySQL 8.0+ / PostgreSQL 12+
- Composer 2.x
- Node.js 18+ (for frontend assets)

## Installation

```bash
# Clone the repository
git clone https://github.com/calounx/chom.git
cd chom

# Install dependencies
composer install

# Copy environment file
cp .env.example .env

# Generate application key
php artisan key:generate

# Run migrations
php artisan migrate

# Start the development server
php artisan serve
```

## Configuration

### Environment Variables

```env
# Database
DB_CONNECTION=sqlite
DB_DATABASE=/path/to/database.sqlite

# VPS Manager SSH
CHOM_SSH_KEY_PATH=storage/app/ssh/chom_deploy_key

# Observability Stack
CHOM_PROMETHEUS_URL=http://prometheus:9090
CHOM_LOKI_URL=http://loki:3100
CHOM_GRAFANA_URL=http://grafana:3000
CHOM_GRAFANA_API_KEY=your-api-key
```

## Architecture

```
┌─────────────────────────────────────────────────────────┐
│           SaaS Control Plane (Laravel)                  │
│  ┌─────────────────────────────────────────────────┐   │
│  │ Dashboard (Livewire) │ REST API (Sanctum)       │   │
│  └──────────────────────┴──────────────────────────┘   │
│  ┌─────────────────────────────────────────────────┐   │
│  │ Services: VPSManagerBridge, ObservabilityAdapter│   │
│  └─────────────────────────────────────────────────┘   │
└───────────────────────────┬─────────────────────────────┘
                            │ SSH + HTTP
        ┌───────────────────┼───────────────────┐
        ▼                   ▼                   ▼
┌──────────────┐   ┌────────────────┐   ┌─────────────┐
│  VPSManage   │   │ Observability  │   │   Stripe    │
│  (SSH+CLI)   │   │ Stack (HTTP)   │   │  (Webhooks) │
└──────────────┘   └────────────────┘   └─────────────┘
```

## Pricing Tiers

| Tier | Price | Sites | Storage | Features |
|------|-------|-------|---------|----------|
| Starter | $29/mo | 5 | 10GB | SSL, Daily backups |
| Pro | $79/mo | 25 | 100GB | + Staging, Priority support |
| Enterprise | $249/mo | Unlimited | Unlimited | + White-label, Dedicated IP |

## API Documentation

### Authentication

```bash
# Register
POST /api/v1/auth/register

# Login
POST /api/v1/auth/login

# Get current user
GET /api/v1/auth/me
```

### Sites

```bash
# List sites
GET /api/v1/sites

# Create site
POST /api/v1/sites

# Issue SSL
POST /api/v1/sites/{id}/ssl
```

### Backups

```bash
# List backups
GET /api/v1/backups

# Create backup
POST /api/v1/sites/{id}/backups

# Restore backup
POST /api/v1/backups/{id}/restore
```

## Development

```bash
# Run tests
php artisan test

# Clear caches
php artisan optimize:clear

# Run queue worker
php artisan queue:work
```

## Security

- All API endpoints use Laravel Sanctum for token-based authentication
- Rate limiting: 5 req/min for auth, 60 req/min for API, 10 req/min for sensitive operations
- SSH connections use key-based authentication
- Prometheus/Loki queries are tenant-scoped to prevent data leakage

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Support

For support, please contact support@chom.io
