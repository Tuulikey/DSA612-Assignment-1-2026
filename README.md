# DSA612-Assignment-1-2026


A two-part distributed systems project: a REST API for tracking library/campus resources across institutions, and a gRPC-based rental accommodation platform with a web frontend.

## Table of Contents
- Overview
- Features
- Tech Stack
- Project Structure
- Data Model
- Getting Started
- Testing
- Known Issues
- Build Status

## Overview

**Library Management System (Q1 — REST):** A shared system for tracking books, electronic resources, and physical spaces (labs, meeting rooms) across multiple institutions and campuses. Supports full CRUD, institution/site filtering, maintenance and overdue checks, component tracking, servicing schedules, and work orders with sub-tasks. Includes a Ballerina CLI client.

**Rent-A-Hun (Q2 — gRPC):** A platform connecting Hosts and Guests for short-term property rentals. Hosts list and manage properties; Guests browse, search, and book accommodation for specific dates, with server-side validation for date overlaps and cost calculation. Includes a Ballerina gRPC client and a Next.js web interface.

## Features

**Library Management System**
- Asset CRUD — create, update, look up, and remove resources
- Institution & site filtering
- Overdue & maintenance dashboard
- Component management for complex assets
- Servicing schedule management
- Work orders with sub-tasks
- CLI client — loaning, global/campus views, overdue dashboard, schedule management

**Rent-A-Hun**
- Property listing, update, and removal (Host)
- Bulk user onboarding via client-side streaming
- Server-streamed property browsing, filterable by location/price
- Property search by ID
- Booking cart with check-in/check-out validation
- Booking confirmation — overlap checking and total cost calculation
- Web app for Hosts (dashboard, add-property) and Guests (browse, cart, bookings)

## Tech Stack

| Layer | Technology |
|---|---|
| Q1 Backend & Client | Ballerina, REST/HTTP |
| Q2 Backend | Ballerina, gRPC (Protocol Buffers) |
| Q2 Web Frontend | Next.js, TypeScript, Drizzle |
| Storage | In-memory Map/Table (Ballerina); DB via Drizzle (Q2 web) |

## Project Structure

```
DSA612-Assignment-1-2026/
├── Library Management System/
│   ├── index.html
│   ├── handles-requests.http
│   └── modules/
│       ├── library_client/       # CLI client
│       └── library_service/      # REST service
│
└── Rent-A-Hun/
    ├── proto/
    │   └── rental_accommodation.proto
    ├── ballerina/
    │   ├── server.bal
    │   ├── happy_client/         # gRPC client
    │   ├── server_service/       # gRPC server
    │   └── stubs/
    └── src/
        ├── app/
        │   ├── api/               # bookings, cart, properties, stats, users
        │   ├── guest/              # browse, cart, bookings, property/[id]
        │   └── host/                # dashboard, add-property
        ├── components/
        └── db/
```

## Data Model

**Asset (Library Management System)**
| Field | Type | Description |
|---|---|---|
| assetTag | String (unique key) | Unique identifier |
| name, description | String | Asset details |
| institution, site | String | Location |
| status | String | AVAILABLE / LOANED_OUT / UNDER_MAINTENANCE / DISPOSED |
| dateAcquired | Date | Acquisition date |
| components, schedules, workOrders | List | Nested records |

**Property (Rent-A-Hun)**
| Field | Type | Description |
|---|---|---|
| property_id | String (unique key) | Auto-generated |
| name, location, property_type | String | Listing details |
| price_per_night | Decimal | Nightly rate |
| status | String | Availability |

## Getting Started

**Library Management System**
```
cd "Library Management System/modules/library_service"
bal run
```
```
cd "Library Management System/modules/library_client"
bal run
```

**Rent-A-Hun — gRPC backend**
```
cd Rent-A-Hun/ballerina/server_service
bal run
```
```
cd Rent-A-Hun/ballerina/happy_client
bal run
```

**Rent-A-Hun — Web app**
```
cd Rent-A-Hun
npm install
npm run dev
```

## Testing

Both systems were tested end-to-end before submission:
- Library Management System: all CRUD, filtering, overdue/maintenance checks, component, schedule, and work order endpoints verified via `handles-requests.http` and the CLI client
- Rent-A-Hun: all gRPC methods (simple, client-streaming, server-streaming) verified via the Ballerina client; booking overlap validation and cost calculation confirmed; web app flows tested for both Host and Guest roles

## Known Issues

- None outstanding at time of submission.

## Build Status

| Component | Status |
|---|---|
| Library — Data model & service setup | Done |
| Library — CRUD, filtering, overdue checks | Done |
| Library — Work orders, components, schedules | Done |
| Library — CLI client | Done |
| Rent-A-Hun — .proto contract | Done |
| Rent-A-Hun — gRPC server (properties, bookings) | Done |
| Rent-A-Hun — gRPC client | Done |
| Rent-A-Hun — Next.js web app | Done |
| Testing | Done |
| Documentation | Done |
