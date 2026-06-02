# QMOS - Technical Architecture & Engineering Specification

# Project Goal

Build a production-grade Community Operating System capable of serving:

- 200–500 active students
- Multiple communities/clubs
- Simultaneous quiz participation
- Event registrations
- Attendance management
- Resource sharing
- Certificate generation

while remaining:

- Lightweight
- Secure
- Scalable
- Maintainable
- Mobile-friendly

---

# Architecture Overview

```text
Frontend (React)
       │
       ▼
API Gateway (Express)
       │
       ▼
Business Layer
       │
       ▼
PostgreSQL Database

       │
       ├── Storage (Files / Certificates)
       │
       └── Notification Service
```

Architecture Style:

- Monolithic Backend
- Modular Design
- REST APIs
- Feature-Based Structure

Reason:

For 200-500 users, a well-designed monolith is simpler and more maintainable than microservices.

---

# Tech Stack

## Frontend

- React 19
- TypeScript
- Vite
- Tailwind CSS
- ShadCN UI
- React Router
- Zustand
- TanStack Query
- React Hook Form
- Zod
- Recharts

---

## Backend

- Node.js
- Express.js
- TypeScript
- JWT
- Bcrypt

---

## Database

- PostgreSQL

Reason:

Strong relationships.

Supports:

- Analytics
- Aggregations
- Full Text Search
- Transactions

Perfect for QMOS.

---

## File Storage

Supabase Storage

Used For:

- Certificates
- Event Posters
- Community Logos
- Resources

---

## Deployment

Frontend:

- Vercel

Backend:

- Railway
  or
- Render

Database:

- PostgreSQL

---

# Folder Structure

## Frontend

```text
src/
│
├── app/
│
├── routes/
│
├── pages/
│
├── features/
│   ├── auth/
│   ├── community/
│   ├── events/
│   ├── quizzes/
│   ├── certificates/
│   ├── leaderboard/
│   └── resources/
│
├── components/
│
├── hooks/
│
├── services/
│
├── store/
│
├── utils/
│
└── types/
```

---

## Backend

```text
src/
│
├── modules/
│   ├── auth/
│   ├── users/
│   ├── communities/
│   ├── events/
│   ├── quizzes/
│   ├── certificates/
│   ├── notifications/
│   └── analytics/
│
├── middleware/
│
├── config/
│
├── database/
│
├── utils/
│
├── jobs/
│
└── server.ts
```

---

# Authentication

System:

JWT Access Token

-

Refresh Token

Flow:

```text
Login

↓

Access Token

↓

API Request

↓

Token Expired

↓

Refresh Token

↓

New Access Token
```

Benefits:

- Secure
- Scalable
- Industry Standard

---

# Authorization

RBAC

(Role Based Access Control)

Roles:

```text
Super Admin

Faculty

Community Admin

Core Team Member

Student
```

Example:

Student:

- Join Event
- Take Quiz

Community Admin:

- Create Event
- Create Quiz
- Generate Certificates

---

# Database Design

## users

```text
id
name
email
password_hash
role
avatar
created_at
```

---

## communities

```text
id
name
description
logo
created_by
```

---

## community_members

```text
user_id
community_id
role
joined_at
```

---

## events

```text
id
community_id
title
description
location
capacity
date
status
```

---

## event_registrations

```text
id
user_id
event_id
status
registered_at
```

---

## attendance

```text
id
event_id
user_id
checked_in_at
```

---

## quizzes

```text
id
community_id
title
duration
start_time
end_time
```

---

## questions

```text
id
quiz_id
question
option_a
option_b
option_c
option_d
correct_option
```

---

## submissions

```text
id
quiz_id
user_id
score
submitted_at
```

---

## resources

```text
id
community_id
title
file_url
resource_type
```

---

## certificates

```text
id
user_id
event_id
certificate_url
```

---

## announcements

```text
id
community_id
title
content
created_at
```

---

# Search System

Students can search:

- Events
- Communities
- Resources

Implementation:

PostgreSQL Full Text Search

Benefits:

- Fast
- Lightweight
- No Elasticsearch required

---

# State Management

## Zustand

Use For:

- Auth State
- Theme State
- User Preferences

Do NOT store server data.

---

# Server State

## TanStack Query

Use For:

- Events
- Quizzes
- Communities
- Announcements

Benefits:

- Caching
- Refetching
- Reduced API calls

---

# Forms

React Hook Form

-

Zod

Benefits:

- Fast
- Minimal Re-renders
- Type Safe Validation

---

# Quiz System Optimization

For 200+ users:

Questions fetched once.

Auto-save every:

```text
30 seconds
```

Submission transaction:

```text
BEGIN

Store Answers

Calculate Score

Save Submission

COMMIT
```

Prevents corruption.

---

# Attendance System

Method:

QR Code

Flow:

```text
Student Opens QR

↓

Scan

↓

Validate Event

↓

Mark Attendance

↓

Success
```

Reduces manual work.

---

# Certificate Generation

Generate PDF automatically.

Contains:

- Name
- Event
- Date
- Certificate ID

Stored in Storage Bucket.

---

# Notification System

Version 1

In-App Notifications

Tables:

```text
notifications
```

Version 2

Email Notifications

Can be added later.

---

# Analytics Dashboard

Community Admin sees:

- Total Members
- Event Registrations
- Attendance %
- Quiz Participation
- Most Active Members

---

# Performance Optimization

## Pagination

Never fetch:

```text
1000 rows
```

Instead:

```text
20 rows/page
```

---

## Lazy Loading

Load pages only when needed.

---

## Image Optimization

Use:

- WebP
- Compression

---

## API Compression

Enable GZIP.

---

## React Query Cache

Reduces repeated requests.

---

## Database Indexes

Create indexes on:

```sql
users(email)

events(community_id)

event_registrations(event_id)

attendance(event_id)

submissions(user_id)
```

---

# Security

## Password Hashing

bcrypt

Never store raw passwords.

---

## SQL Injection Prevention

Parameterized Queries

Never use string concatenation.

---

## Rate Limiting

Protect:

- Login
- Registration
- Quiz Submission

---

## Helmet

Secure HTTP Headers

---

## CORS

Allow only trusted domains.

---

## Input Validation

Zod

Every API request validated.

---

# Scalability

Target:

200–500 Active Users

Expected Capacity:

- 50+ Communities
- 10,000+ Registrations
- Thousands of Quiz Attempts

PostgreSQL easily handles this scale.

---

# Future Features

Phase 2

- Mobile App
- Push Notifications
- Event Check-In App
- Community Reputation Score
- AI Event Recommendations

---

# Resume Value

This project demonstrates:

✓ Authentication

✓ Authorization

✓ Database Design

✓ PostgreSQL

✓ API Design

✓ Search

✓ Analytics

✓ File Storage

✓ Performance Optimization

✓ Security

✓ Deployment

✓ Real User Product Development

This is significantly stronger than typical student projects and can become a flagship internship project.
