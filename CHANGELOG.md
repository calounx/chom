# Changelog

All notable changes to CHOM will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.0] - 2025-12-27

### Added

#### Core Platform
- Multi-tenant architecture with Organizations, Tenants, and Users
- Role-based access control (Owner, Admin, Member, Viewer)
- Laravel 12 with Livewire for reactive UI
- Laravel Sanctum for API authentication

#### Site Management
- WordPress site provisioning
- HTML/static site support
- Laravel site support
- SSL certificate issuance and renewal
- PHP version management (8.2, 8.4)

#### VPS Management
- VPS fleet management with automatic allocation
- Shared and dedicated VPS allocation types
- Health monitoring and status tracking
- SSH-based command execution via VPSManagerBridge

#### Backup System
- Full, files-only, and database-only backups
- Configurable retention policies per tier
- Backup restoration with confirmation
- Async job processing for long operations

#### Observability Integration
- Prometheus metrics querying with tenant isolation
- Loki log aggregation with tenant scoping
- Grafana dashboard embedding
- Real-time metrics dashboard

#### Team Management
- Team member invitation system
- Role assignment and management
- Organization ownership transfer
- Audit logging for team actions

#### API
- RESTful API v1 with versioned endpoints
- Rate limiting (auth: 5/min, api: 60/min, sensitive: 10/min)
- Comprehensive error responses with codes
- Pagination and filtering support

#### Billing (Prepared)
- Stripe integration ready (Laravel Cashier)
- Three pricing tiers: Starter ($29), Pro ($79), Enterprise ($249)
- Usage metering infrastructure
- Invoice tracking

### Security
- Query injection prevention in ObservabilityAdapter
- Command whitelist for VPS operations
- SSH key permission validation
- Password hashing for team invitations
- Authorization policies for all resources
- Hidden sensitive model attributes

### Database
- 17 migrations with proper foreign key constraints
- UUID primary keys throughout
- Soft deletes for sites
- Audit log infrastructure

### Performance
- N+1 query optimizations in Livewire components
- Cached backup size calculations
- Optimized aggregation queries
- Async job queuing for long operations

## [Unreleased]

### Planned
- Email verification flow
- Password reset functionality
- Two-factor authentication
- Staging environment support
- White-label customization
- Custom domain SSL via Let's Encrypt
- Automated backup scheduling
- Alert management UI
