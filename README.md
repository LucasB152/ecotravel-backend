# EcoTravel — Backend

> Bachelor team project for the *Software Architecture* course (3 students, Nov. 2024 – Jan. 2025) · **Archived, not maintained**

EcoTravel is a fictional platform built for a course project. It lists **eco-friendly accommodations and activities** and lets travellers combine them into **itineraries**. The original goal was also to estimate the CO₂ footprint of each itinerary.

This repository contains the **REST API**. The Angular client is in [ecotravel-frontend](https://github.com/LucasB152/ecotravel-frontend).

## Project status

The project was delivered at the end of the course and has not been worked on since. **Some features are incomplete**. In particular, the CO₂ estimation of itineraries was never implemented, and there are almost no automated tests.

## Features

- **Authentication**: sign-up, email verification, login with JWT
- **Roles**: traveller, host and admin. A user can request a host account, and an admin approves or rejects the request
- **Destinations**: hosts create, edit and delete accommodations and activities, with pictures and tags. Addresses are geocoded with the Google Maps API
- **Search** for destinations by type and tags
- **Reviews** on destinations
- **Itineraries**: create an itinerary, add, remove and reorder its steps
- **Admin**: manage host requests and user roles

## Tech stack

| | |
|---|---|
| Language | Java 21 |
| Framework | Spring Boot (Web, Data JPA, Security, Validation, Mail) |
| Database | PostgreSQL |
| Auth | JWT (jjwt) |
| Mapping | MapStruct |
| External services | Cloudinary (images), Google Maps Geocoding, Brevo (SMTP) |
| API docs | springdoc-openapi (Swagger UI) |
| Build / deploy | Gradle, Docker |

## Running locally

Requirements: Java 21 and a PostgreSQL database, or Docker.

The configuration is read from environment variables:

| Variable | Description |
|---|---|
| `DB_URL`, `DB_USERNAME`, `DB_PASSWORD` | PostgreSQL connection |
| `JWT_SECRET_KEY` | Key used to sign the JWT tokens |
| `URL_FRONT` | URL of the frontend (CORS and email links) |
| `MAIL_USERNAME`, `MAIL_PASSWORD` | SMTP credentials |
| `CLOUD_NAME`, `CLOUD_KEY`, `CLOUD_SECRET` | Cloudinary credentials |

```bash
./gradlew bootRun
```

or with Docker:

```bash
docker build -t ecotravel-back .
docker run -p 8081:8081 --env-file .env ecotravel-back
```

The API runs on port `8081`. The Swagger UI is available at `http://localhost:8081/swagger-ui.html`.

## API overview

| Prefix | Purpose |
|---|---|
| `/api/auth` | Sign-up, login, email verification |
| `/api/user` | Profile, password, profile picture |
| `/api/host` | Host destinations (CRUD) |
| `/api/destination` | Destination details, pictures, types |
| `/api/tag` | Tags |
| `/api/review` | Reviews |
| `/api/itinerary`, `/api/step` | Itineraries and their steps |
| `/api/request` | Host account requests |
| `/api/admin` | Administration |
