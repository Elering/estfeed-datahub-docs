# REST API Versioning and Maintenance Policy

- [Introduction](#introduction)
- [Versioning Principles](#versioning-principles)
- [API Lifecycle Stages](#api-lifecycle-stages)
- [Transition Periods](#transition-periods)
- [Migration Guidelines](#migration-guidelines)
- [Notifications](#notifications)
- [API versions and transition deadlines](#api-versions-and-transition-deadlines)

## Introduction

This document describes the versioning strategy for the Estfeed Datahub REST APIs, including lifecycle stages, deprecation timelines, and transition rules.

## Versioning Principles

- REST APIs are versioned using a **major version number** in the URL:
  - Example:  
    - `https://datahub.elering.ee/api/v1/...`  
    - `https://datahub.elering.ee/api/v2/...`

- **Minor changes** (non-breaking) may be introduced without creating a new version.  
- **Breaking changes** always result in a new major version.

## API Lifecycle Stages

Each API version goes through the following stages:

1. **Active** – Fully supported and maintained.  
2. **Deprecated** – Still accessible but scheduled for shutdown.  
3. **Retired** – Disabled and no longer accessible.

## Transition Periods

- A **minimum 6-month transition window** is guaranteed after a version is marked as *Deprecated*.   
- During this period both old and new versions run in parallel. 

## Migration Guidelines

- Always start new integrations with the **latest active version**.    
- If using a deprecated version:
  - Plan migration **before the retirement date**.  
  - Follow the published migration guides if any for smooth transition.  
- Detailed information regarding the versions can be found from this documentation and from Swagger.

## Notifications

- All version changes are communicated via:
  - Email is sent to administrators that are marked in the agreement.
  - Changes are documented in Github.
  - API error headers (where applicable). 
- Breaking changes will **never** be introduced without announcing a deprecation timeline.


## API versions and transition deadlines

| Type | Endpoint | Version | Status | Valid from date | Deprecated date | Retirement Date | Notes |
|------|-----------|----------|---------|------------------|-------------------|-------------------|-------------|
| POST | /api/v1/agreement | v1 | deprecated | 22.11.2024 | 17.09.2025 | 31.03.2026 | Transition to v2 required. |
| POST | /api/v2/agreements | v2 |  active | 17.09.2025 | - | - |  |
| POST | /api/v1/agreement/search | v1 | deprecated | 22.11.2024 | 17.09.2025 | 31.03.2026 | Transition to v2 required. |
| GET | /api/v2/agreements | v2 | active | 17.09.2025 | - | - |  |
| GET | /api/v2/agreements/{id} | v2 | active | 17.09.2025 | - | - |  |
| POST | /api/v1/agreement/search/meter | v1 | deprecated | 22.11.2024 | 17.09.2025 | 31.03.2026 | Transition to v2 required. |
| GET | /api/v2/metering-points/{eic}/agreements | v2 | active | 17.09.2025 | - | - |  |
| POST | /api/v1/agreement/export | v1 | deprecated | 22.11.2024 | 17.09.2025 | 31.03.2026 | Transition to v2 required. |
| GET | /api/v2/agreements/export | v2 | active | 17.09.2025 | - | - |   |
| POST | /api/v1/agreement/delete | v1 | deprecated | 22.11.2024 | 17.09.2025 | 31.03.2026 | Transition to v2 required. |
| DELETE | /api/v2/agreements/{id} | v2 | active | 17.09.2025 | - | - |  |
| POST | /api/v1/agreement-bulk | v1 | deprecated | 22.11.2024 | 17.09.2025 | 31.03.2026 | Transition to v2 required. |
| POST | /api/v2/agreements/bulk | v2 | active | 17.09.2025 | - | - |  |
| PUT | /api/v1/agreement | v1 | deprecated | 22.11.2024 | 17.09.2025 | 31.03.2026 | Transition to v2 required. |
| PUT | /api/v2/agreements/{id} | v2 | active | 17.09.2025 | - | - |  |
| PUT | /api/v2/agreements/{id} | v2 | active | 17.09.2025 | - | - |  |
| POST | /api/v1/template/meter | v1 | active | 22.11.2024 | - | - |  |
| PUT | /api/v1/meter | v1 | active | 22.11.2024 | - | - |  |
| POST | /api/v1/meter | v1 | active | 22.11.2024 | - | - |  |
| POST | /api/v1/meter/search | v1 | active | 22.11.2024 | - | - |  |
| POST | /api/v1/meter/search/customer | v1 | active | 22.11.2024 | - | - |  |
| POST | /api/v1/meter/search/border | v1 | active | 22.11.2024 | - | - |  |
| POST | /api/v1/meter/import | v1 | active | 22.11.2024 | - | - |  |
| POST | /api/v1/meter/export | v1 | active | 22.11.2024 | - | - |  |
| POST | /api/v1/meter/eic/amount | v1 | active | 22.11.2024 | - | - |  |
| POST | /api/v1/meter/eic/range | v1 | active | 22.11.2024 | - | - |  |
| POST | /api/v1/meter-data | v1 | active | 22.11.2024 | - | - |  |
| POST | /api/v1/meter-data/status | v1 | active | 22.11.2024 | - | - |  |
| POST | /api/v1/meter-data/search | v1 | active | 22.11.2024 | - | - |  |
| POST | /api/v1/meter-data/import | v1 | active | 22.11.2024 | - | - |  |
| POST | /api/v1/meter-data/export | v1 | active | 22.11.2024 | - | - |  |
| POST | /api/v1/template/meter-data | v1 | active | 22.11.2024 | - | - |  |
| POST | /api/v1/authorization | v1 | active | 22.11.2024 | - | - |  |
| POST | /api/v1/user/rights/search | v1 | active | 22.11.2024 | - | - |  |
| GET | /api/v1/user-role-type | v1 | active | 22.11.2024 | - | - |  |
| GET | /api/v1/user/market-roles | v1 | active | 22.11.2024 | - | - |  |
| POST | /api/v1/network-bill | v1 | active | 22.11.2024 | - | - |  |
| POST | /api/v1/network-bill/search | v1 | active | 22.11.2024 | - | - |  |
| POST | /api/v1/joint-invoice | v1 | active | 22.11.2024 | - | - |  |
| POST | /api/v1/joint-invoice/search | v1 | active | 22.11.2024 | - | - |  |
| POST | /api/v1/joint-invoice/download | v1 | active | 22.11.2024 | - |- |  |
| POST | /api/v1/customer-authorization/search | v1 | active | 22.11.2024 | - | - |  |
| POST | /api/v1/connection-state/search | v1 | active | 22.11.2024 | - | - |  |
| POST | /api/v1/connection-state/message | v1 | active | 22.11.2024 | - | - |  |
| POST | /api/v1/connection-state/message-history | v1 | active | 22.11.2024 | - | - |  |
| POST | /api/v1/connection-state/initiate | v1 | active | 22.11.2024 | - | - |  |
| POST | /api/v1/authorization/search | v1 | active | 22.11.2024 | - | - |  |
| PUT | /api/v1/authorization/delete | v1 | active | 22.11.2024 | - | - |  |
| POST | /api/v1/customer | v1 | active | 22.11.2024 | - | - |  |
| POST | /api/v1/customer/search | v1 | active | 22.11.2024 | - | - |  |
| PUT | /api/v1/idr/technical-user | v1 | active | 22.11.2024 | - | - |  |
| POST | /api/v1/idr/technical-user/search | v1 | active | 22.11.2024 | - | - |  |
| POST | /api/v1/idr/technical-user/role | v1 | active | 22.11.2024 | - | - |  |
| POST | /api/v1/balance-settlement-point/search | v1 | active | 22.11.2024 | - | - |  |
| POST | /api/v1/report/export/json | v1 | active | 22.11.2024 | - | - |  |
| POST | /api/v1/report/export/excel | v1 | active | 22.11.2024 | - | - |  |
| POST | /api/v1/report/search | v1 | active | 22.11.2024 | - | - |  |
| PUT | /api/v1/joint-invoice | v1 | active | 22.11.2024 | - | - |  |
| POST | /api/v1/data-distribution/search | v1 | active | 22.11.2024 | - | - | Starting from 31.02.2026 this can't be used for agreement related messages. |
| GET | /api/v2/data-distributions/agreement | v2 | active | 17.09.2025 | - | - |  |




