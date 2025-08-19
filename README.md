# Hotel Booking Platform — Node.js, React, REST API, Docker

[![Releases](https://img.shields.io/badge/Release-download-blue?logo=github&label=Releases)](https://github.com/Kelmada/Hotel-booking/releases)

![Hotel hero image](https://images.unsplash.com/photo-1501117716987-c8e6b7f8b0f0?auto=format&fit=crop&w=1600&q=60)

https://github.com/Kelmada/Hotel-booking/releases

Overview
- A full-stack hotel booking system.
- Backend: Node.js, Express, PostgreSQL using an ORM.
- Frontend: React with React Router and a simple state layer.
- Delivery: Docker images and release artifacts.
- API: REST endpoints for rooms, bookings, users, and payments.

Badges
- Build: GitHub Actions (CI).
- Coverage: 90% test coverage target.
- Releases: Click the badge above or visit the Releases page.

Quick links
- Releases page: https://github.com/Kelmada/Hotel-booking/releases (download the release file and execute it)
- Issues: Use GitHub Issues to report bugs or request features.
- Pull requests: Open PRs against the main branch.

What this repo contains
- /server — Node.js API, routes, controllers, services, and DB migrations.
- /client — React app, pages, components, and hooks.
- /docker — Dockerfiles and compose files for local dev.
- /scripts — helpers for setup, seed, and migration.
- /docs — API reference and sequence diagrams.
- /tests — unit and integration tests.

Screenshots
![Booking list](https://images.unsplash.com/photo-1519710164239-da123dc03ef4?auto=format&fit=crop&w=1200&q=60)
![Room detail](https://images.unsplash.com/photo-1505691723518-36a81a8a7a2b?auto=format&fit=crop&w=1200&q=60)

Features
- Search rooms by date, capacity, and amenities.
- Create, update, and cancel reservations.
- User authentication with JWT.
- Admin dashboard for room and booking management.
- Rate limits and input validation on all public endpoints.
- Payment integration stub for card and invoice flows.
- Email notifications for booking events.
- Basic analytics for occupancy and revenue.

Architecture
- API: RESTful design. Controllers remain thin. Business rules live in services.
- Persistence: PostgreSQL. Migrations with SQL-based scripts.
- Frontend: Single Page App. Component-based UI and modular CSS.
- Deployment: Docker images for server and client, orchestrated by Docker Compose or Kubernetes.
- Observability: Central logs, structured JSON output, and health endpoints.

Getting started - run locally with Docker
1. Clone the repo:
   - git clone https://github.com/Kelmada/Hotel-booking.git
2. Copy environment template:
   - cp .env.example .env
3. Start with Docker Compose:
   - docker-compose up --build
4. Open the client at http://localhost:3000
5. API runs at http://localhost:4000/api

Install release artifact
- Visit the Releases page or click the Releases badge above: https://github.com/Kelmada/Hotel-booking/releases
- Download the artifact that matches your platform, for example:
  - hotel-booking-linux-x64.tar.gz
  - hotel-booking-win-x64.zip
  - hotel-booking-macos-arm64.tar.gz
- Extract the archive.
- Execute the binary or start script:
  - linux / mac: ./hotel-booking && open http://localhost:4000
  - windows: hotel-booking.exe and open http://localhost:4000
- The release includes embedded config defaults and a minimal SQLite DB for quick demos.

API reference (high level)
- Authentication
  - POST /api/auth/register — create user
  - POST /api/auth/login — obtain JWT
- Rooms
  - GET /api/rooms — list rooms with filters
  - GET /api/rooms/:id — room details
  - POST /api/rooms — create room (admin)
  - PUT /api/rooms/:id — update room (admin)
- Bookings
  - POST /api/bookings — create booking
  - GET /api/bookings/:id — booking detail
  - PUT /api/bookings/:id — modify booking
  - DELETE /api/bookings/:id — cancel booking
- Payments
  - POST /api/payments — charge a booking
- Health
  - GET /api/health — service status

Authentication and security
- JWT tokens sign session data.
- Passwords use salted hashing (bcrypt).
- Role-based access: user, admin.
- Input sanitization on server.
- Rate limiter applied on login and booking endpoints.

Database and schema
- Entity model:
  - User: id, name, email, passwordHash, role
  - Room: id, number, type, capacity, price, amenities
  - Booking: id, userId, roomId, fromDate, toDate, status, total
  - Payment: id, bookingId, amount, currency, status
- Migrations live in /server/migrations.
- Seed scripts create sample rooms and demo users.

Development workflow
- Branch model: feature/* for features, fix/* for fixes.
- Pull requests require code review and passing CI.
- Linting: ESLint for JS and Prettier for formatting.
- Tests: Jest for unit tests, Supertest for API integration.

Testing
- Run all tests:
  - npm run test
- Run server tests:
  - cd server && npm run test
- Run client tests:
  - cd client && npm run test
- Tests include unit coverage and basic end-to-end flows with an in-memory DB.

Continuous integration
- CI runs on push to main and on PR.
- CI tasks:
  - Install and lint
  - Run unit tests
  - Build Docker images
  - Publish artifacts to Releases on tag

Docker
- docker/Dockerfile.server — production-ready server image.
- docker/Dockerfile.client — static client build.
- docker/docker-compose.yml — compose file for local dev
- Commands:
  - docker build -t hotel-booking-server -f docker/Dockerfile.server .
  - docker run -p 4000:4000 hotel-booking-server

Deployment
- Provide two options:
  - Kubernetes: Helm chart available in /deploy/helm
  - Docker Compose: docker-compose.prod.yml for a simple host
- Use secrets management for DB credentials and JWT secret in production.

UI notes
- Component library: simple design system with buttons, inputs, cards.
- Pages:
  - Home / Search
  - Room list
  - Room detail
  - Booking flow with calendar picker
  - User profile and bookings
  - Admin dashboard for room and booking management

Performance and scaling
- Use DB indexes on booking dates and room ids.
- Cache room list with a short TTL.
- Use background workers for email and heavy tasks.
- Scale API with replicas behind a load balancer.

Observability
- Expose /api/health for checks.
- Structured logs output as JSON.
- Error tracking integration can be enabled via env var.

Common tasks
- Run migrations:
  - npm run migrate
- Seed data:
  - npm run seed
- Start server in dev:
  - npm run dev
- Build client:
  - cd client && npm run build

Contributing
- Open an issue to start a discussion.
- Fork and create a branch with a clear name.
- Include tests for new features.
- Keep commits small and focused.
- Use descriptive PR titles and include a changelog entry.

Maintainers
- Repo maintainer: Kelmada
- How to reach: use GitHub Issues and mention @Kelmada on PRs

License
- MIT License. See LICENSE file.

Roadmap
- Add payment gateway integration (Stripe).
- Add multi-currency support.
- Add mobile app skeleton.
- Add more automated checks in CI.

Files to check first
- server/src/index.js — API entry point
- client/src/App.jsx — main app
- docker/docker-compose.yml — compose for dev
- README.md — this file
- docs/api.md — full API docs and examples

If the Releases link does not work
- Visit the Releases section on GitHub from the repository main page.
- The Releases page contains packaged artifacts and install notes.

Command reference summary
- Local dev:
  - git clone https://github.com/Kelmada/Hotel-booking.git
  - cp .env.example .env
  - docker-compose up --build
- Release install:
  - Download from https://github.com/Kelmada/Hotel-booking/releases and execute the provided binary or script

Quick troubleshooting
- If the app cannot connect to the DB:
  - Check DB env vars in .env
  - Ensure Docker Compose started the db service
- If builds fail:
  - Run linters locally: npm run lint
  - Run tests: npm run test

API usage example (curl)
- Login:
  - curl -X POST http://localhost:4000/api/auth/login -d '{"email":"demo@example.com","password":"demo"}' -H "Content-Type: application/json"
- List rooms:
  - curl http://localhost:4000/api/rooms

Contact and support
- Open an issue for bugs or feature requests.
- Use PRs for code contributions.
- Check the Releases page for packaged builds and installers: https://github.com/Kelmada/Hotel-booking/releases

Acknowledgements
- Icons from Feather Icons.
- Images from Unsplash.
- Docker and Node.js ecosystems for tooling and libraries.