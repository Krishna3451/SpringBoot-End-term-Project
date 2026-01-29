# 🎫 Event Booking Platform

<div align="center">

![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.4.1-brightgreen?style=for-the-badge&logo=springboot)
![Java](https://img.shields.io/badge/Java-21-orange?style=for-the-badge&logo=openjdk)
![PostgreSQL](https://img.shields.io/badge/PostgreSQL-15-blue?style=for-the-badge&logo=postgresql)
![Redis](https://img.shields.io/badge/Redis-7-red?style=for-the-badge&logo=redis)
![Kafka](https://img.shields.io/badge/Apache%20Kafka-7.5-black?style=for-the-badge&logo=apachekafka)
![Docker](https://img.shields.io/badge/Docker-Ready-blue?style=for-the-badge&logo=docker)

**A production-grade event booking and ticketing platform built with Spring Boot**

[Features](#-features) • [Tech Stack](#-tech-stack) • [Getting Started](#-getting-started) • [API Documentation](#-api-documentation) • [Architecture](#-architecture)

</div>

---

## 📋 Overview

Event Booking Platform is a comprehensive solution for managing events, venues, bookings, and ticket sales. It provides a robust backend with features like JWT authentication, payment processing, real-time notifications, and analytics.

---

## ✨ Features

### 🔐 Authentication & Security
- JWT-based authentication with role-based access control
- Secure password hashing with BCrypt
- Rate limiting to prevent abuse (Bucket4j)

### 📅 Event Management
- Create, update, and manage events
- Support for multiple ticket types per event
- Event status tracking (Draft, Published, Cancelled, Completed)

### 🏟️ Venue Management
- Register and manage venues
- Track venue capacity and availability

### 🎟️ Booking & Tickets
- Seamless ticket booking flow
- QR code generation for tickets
- Multiple booking statuses (Pending, Confirmed, Cancelled, etc.)

### 💳 Payment Integration
- **Razorpay** payment gateway integration
- Webhook support for payment verification
- Support for refunds and payment tracking

### 📊 Analytics Dashboard
- Event performance metrics
- Revenue tracking
- Booking statistics

### 📧 Notifications
- Email notifications via **SendGrid/Postmark**
- Event-driven architecture with **Kafka** for async processing

### 🖼️ Media Management
- Image uploads via **Cloudinary**
- Support for event banners and venue images

---

## 🛠️ Tech Stack

| Category | Technology |
|----------|------------|
| **Framework** | Spring Boot 3.4.1 |
| **Language** | Java 21 |
| **Database** | PostgreSQL 15 |
| **Caching** | Redis 7 |
| **Message Queue** | Apache Kafka |
| **Authentication** | JWT (jjwt 0.12.6) |
| **Payment** | Razorpay |
| **File Storage** | Cloudinary |
| **Email** | SendGrid |
| **API Docs** | SpringDoc OpenAPI (Swagger UI) |
| **Containerization** | Docker & Docker Compose |

---

## 🚀 Getting Started

### Prerequisites

- Java 21+
- Maven 3.8+
- Docker & Docker Compose (for containerized setup)
- PostgreSQL 15+ (for local setup)

### Option 1: Docker Compose (Recommended)

The easiest way to get started is using Docker Compose:

```bash
# Clone the repository
git clone https://github.com/your-username/event-booking-platform.git
cd event-booking-platform

# Start all services
docker-compose up -d
```

This will start:
- 🖥️ **Application** on port `8080`
- 🐘 **PostgreSQL** on port `5432`
- 🔴 **Redis** on port `6379`
- 📨 **Kafka** on port `9092`
- 🐿️ **Zookeeper** on port `2181`

### Option 2: Local Development

1. **Set up environment variables**

```bash
cp .env.example .env
# Edit .env with your configuration
```

2. **Configure application properties**

The application supports running with or without Redis/Kafka. For local development without Docker:

```bash
# Run with Maven
./mvnw spring-boot:run
```

3. **Database Setup**

Create a PostgreSQL database:
```sql
CREATE DATABASE eventbooking;
```

---

## 🔧 Configuration

### Environment Variables

| Variable | Description | Example |
|----------|-------------|---------|
| `NEON_DB_URL` | PostgreSQL connection URL | `jdbc:postgresql://localhost:5432/eventbooking` |
| `NEON_DB_USERNAME` | Database username | `postgres` |
| `NEON_DB_PASSWORD` | Database password | `your_password` |
| `JWT_SECRET` | JWT signing key (min 256 bits) | `your_secret_key` |
| `RAZORPAY_KEY_ID` | Razorpay API Key ID | `rzp_test_xxx` |
| `RAZORPAY_KEY_SECRET` | Razorpay API Secret | `xxx` |
| `CLOUDINARY_CLOUD_NAME` | Cloudinary cloud name | `your_cloud` |
| `CLOUDINARY_API_KEY` | Cloudinary API key | `xxx` |
| `CLOUDINARY_API_SECRET` | Cloudinary API secret | `xxx` |
| `POSTMARK_SERVER_TOKEN` | Postmark email token | `xxx` |

---

## 📚 API Documentation

Once the application is running, access the interactive API documentation:

- **Swagger UI**: [http://localhost:8080/swagger-ui.html](http://localhost:8080/swagger-ui.html)
- **OpenAPI Spec**: [http://localhost:8080/v3/api-docs](http://localhost:8080/v3/api-docs)

### API Endpoints Overview

| Module | Endpoint | Description |
|--------|----------|-------------|
| **Auth** | `POST /api/auth/register` | User registration |
| | `POST /api/auth/login` | User login |
| **Events** | `GET /api/events` | List all events |
| | `POST /api/events` | Create new event |
| | `GET /api/events/{id}` | Get event details |
| **Venues** | `GET /api/venues` | List all venues |
| | `POST /api/venues` | Create new venue |
| **Bookings** | `POST /api/bookings` | Create booking |
| | `GET /api/bookings/{id}` | Get booking details |
| **Tickets** | `GET /api/tickets/{id}` | Get ticket details |
| | `GET /api/tickets/{id}/qr` | Get ticket QR code |
| **Payments** | `POST /api/payments/create-order` | Create payment order |
| | `POST /api/payments/verify` | Verify payment |
| **Analytics** | `GET /api/analytics/events/{id}` | Event analytics |

---

## 🏗️ Architecture

```
src/main/java/com/eventbooking/
├── 📁 config/          # Configuration classes (Security, Redis, Kafka)
├── 📁 controller/      # REST API controllers
├── 📁 dto/             # Data Transfer Objects
│   ├── request/        # Request DTOs
│   └── response/       # Response DTOs
├── 📁 event/           # Spring application events
├── 📁 exception/       # Custom exceptions & handlers
├── 📁 filter/          # HTTP filters (JWT, Rate Limiting)
├── 📁 kafka/           # Kafka producers & consumers
├── 📁 model/           # JPA entities
│   └── enums/          # Enum types
├── 📁 repository/      # Spring Data JPA repositories
├── 📁 service/         # Business logic services
└── 📁 util/            # Utility classes (QR generation, etc.)
```

### Entity Relationships

```
User ──────┬──────── Booking ────────── Payment
           │              │
           │              └──── Ticket
           │
Event ─────┴──────── TicketType
  │
Venue
```

---

## 🧪 Testing

```bash
# Run all tests
./mvnw test

# Run with coverage
./mvnw test jacoco:report
```

---

## 🐳 Docker

### Build the Image

```bash
docker build -t event-booking-platform .
```

### Run with Docker Compose

```bash
# Start all services
docker-compose up -d

# View logs
docker-compose logs -f app

# Stop all services
docker-compose down
```

---

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

## 👨‍💻 Author

Built with ❤️ as an End-term Project

---

<div align="center">

**[⬆ Back to Top](#-event-booking-platform)**

</div>
