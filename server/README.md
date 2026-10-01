# Server

This directory contains the backend/API layer.

## Responsibilities

- API endpoints
- Business logic
- Data access
- Input validation
- Server-side processing

## Planned Technology

- Node.js
- Express.js
- JavaScript

## Planned API

The first planned API endpoint will provide program catalog data:

GET /api/programs

The endpoint will return program information that the client can display in the Program Catalog feature.

## Architecture Boundary

The server is responsible for providing data and business logic to the client.

The client should not contain the authoritative program catalog data.