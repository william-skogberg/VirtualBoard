# VirtualBoard — Auth API

Node.js, Express, Prisma and PostgreSQL authentication service for the VirtualBoard project. This repository contains the **authentication/backend API**, not the complete board UI.

## Features

- User registration and login with bcrypt password hashes
- Short-lived JWT access tokens and database-backed refresh tokens
- A board created for each new user, with membership-based board listing
- PostgreSQL schema and Prisma migrations

## Run locally

1. Install Node.js and a PostgreSQL database.
2. Run `npm install`.
3. Copy `.env.example` to `.env`, set `DATABASE_URL`, and create a **random, private** `JWT_SECRET`. Do not commit `.env`.
4. Run `npx prisma migrate deploy` (or `npx prisma migrate dev` for local development), then `npx prisma generate`.
5. Run `npm start` (or `npm run dev`). Default port: `4001`.

## API

| Method | Endpoint | Purpose |
| --- | --- | --- |
| GET | `/health` | Health check |
| POST | `/register` | Create user and initial board |
| POST | `/login` | Return access and refresh tokens |
| GET | `/boards` | List boards, requires bearer access token |
| POST | `/refresh` | Exchange valid refresh token for a new access token |
| DELETE | `/refresh` | Revoke refresh token |

Manual request examples are in `test/auth.http` and `test/boards.http`.

## Scope and security

Student project / prototype, not production-ready identity infrastructure. Requires a configured JWT secret; change any old deployment secrets if exposed. For production, review refresh-token storage, rate limiting, input validation, error handling and authentication tests.
