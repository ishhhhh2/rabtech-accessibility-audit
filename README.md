# RabTech Academy Website Audit & Architecture

## Project Overview

This repository contains an accessibility and architecture audit of the RabTech Academy public-facing website.

The project documents accessibility findings, supporting evidence, remediation recommendations, and a proposed monorepo-style project structure for future development.

## Audited Website

RabTech Academy  
https://rabtechacademy.in/

## Audit Scope

The audit covered:

- Lighthouse accessibility checks
- Keyboard-only navigation
- Heading hierarchy
- Color contrast
- HTML structure and landmarks
- Image alternative text
- Interactive element accessibility
- Frontend JavaScript architecture
- Public API usage
- Content rendering patterns

 rabtech-academy-audit/
├── client/
│   └── README.md
├── server/
│   └── README.md
├── docs/
│   ├── README.md
│   ├── docs/accessibility-audit.md
│   ├── accessibility-audit-worksheet.xlsx
│   └── screenshots/
├── tests/
│   └── README.md
└── README.md 


Architecture Boundaries
Client

The client directory represents the frontend application.

Responsibilities:

User interface
Page layouts
Components
Client-side interactions
Accessibility
Communication with backend APIs

Server

The server directory represents the backend/API layer.

Responsibilities:

API endpoints
Business logic
Data access
Validation
Server-side processing

Docs

The docs directory contains project documentation, audit material, architecture notes, and supporting technical documentation.

Tests

The tests directory contains automated and manual test plans for validating application behaviour and accessibility.

Local Setup

The project is currently an architecture skeleton prepared for future implementation.

Prerequisites
Node.js
npm
Git
A code editor such as Visual Studio Code 


Future Setup

The client and server applications can be initialized independently inside their respective directories.

Example:

cd client
npm install

and:

cd server
npm install   


First Vertical Feature Slice

The first planned vertical feature is the Program Catalog.

The feature will connect the frontend and backend through a complete flow:
User
  ↓
Client
  ↓
Program Catalog API
  ↓
Server
  ↓
Program Data
  ↓
Server Response
  ↓
Client UI



Client Responsibility

The client will request program information from the backend and display the available programs in an accessible interface.

Server Responsibility

The server will expose an API endpoint for retrieving program information.

Example future endpoint:

GET /api/programs




Data Responsibility

Program information should be maintained as backend-managed data rather than being embedded directly inside frontend JavaScript.

Audit Findings

The audit identified five issues:

Insufficient color contrast
Non-sequential heading hierarchy
Program catalog content maintained in frontend JavaScript
Promotion API over-fetching for the banner use case
API-provided content rendered through innerHTML 



Detailed evidence and remediation recommendations are documented in:

accessibility-audit.md

The structured accessibility worksheet is:

accessibility-audit-worksheet.xlsx

Audit Evidence

Supporting screenshots are stored in:

screenshots/


These screenshots provide evidence for the documented audit findings.

Status

The repository currently contains the audit documentation and setup-ready architecture skeleton.

Future implementation can build the client, server, automated tests, and complete Program Catalog feature on top of this structure.