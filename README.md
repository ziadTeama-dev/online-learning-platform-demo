# 🎓 Online Learning Platform

A production-oriented online learning platform backend built with **Node.js, Express.js, MongoDB, and REST APIs**.

The platform is designed to support students, teachers, and administrators through secure authentication, role-based authorization, course management, lesson delivery, payments, and other backend services required for an online learning experience.

> 🔒 **This repository is private because the project is being prepared for real-world deployment.**
> The public documentation is provided to showcase the architecture, engineering decisions, and implemented capabilities without exposing production source code or secrets.

---

## 🚀 Overview

The project provides the backend infrastructure for an online learning platform where:

* 👨‍🎓 **Students** can discover courses, enroll, access lessons, and manage their learning experience.
* 👨‍🏫 **Teachers** can create and manage courses and educational content.
* 🛡️ **Administrators** can manage platform-level operations and users.
* 💳 **Payments** can be processed through the configured payment workflow.
* 🔐 **Authentication and authorization** protect platform resources.
* 📦 **File and media handling** supports course-related content.
* 🧪 **Automated tests** help verify critical backend behavior and prevent regressions.

---

## ✨ Core Features

### 🔐 Authentication & Authorization

* User registration and login
* Session-based authentication
* Password hashing with **bcrypt**
* Email verification flow
* Session regeneration for security-sensitive operations
* Role-based authorization
* Resource ownership checks
* Protected routes and middleware

### 👥 User Roles

The platform supports different user roles:

| Role          | Responsibilities                                    |
| ------------- | --------------------------------------------------- |
| 👨‍🎓 Student | Browse courses, enroll, and access learning content |
| 👨‍🏫 Teacher | Create and manage courses and lessons               |
| 🛡️ Admin     | Manage users and platform-level operations          |

---

## 📚 Course Management

The backend supports the core learning entities required by the platform:

* Courses
* Lessons
* Enrollments
* Users
* Payments

Course access can be controlled through enrollment and authorization rules rather than exposing educational resources publicly.

---

## 💳 Payment Integration

The platform includes a payment workflow designed around **Fawry**.

The backend handles payment-related concerns such as:

* Payment creation
* Payment state management
* Request validation
* Webhook processing
* Signature verification
* Idempotency handling
* Protection against invalid payment transitions

The payment flow is designed so that an incoming webhook cannot blindly modify application state without passing the required validation checks.

---

## 📧 Email Verification

User verification is handled through an email-based workflow.

The implementation includes:

* Verification tokens
* Token expiration
* Verification status tracking
* Resending verification emails
* Rate limiting for verification email requests
* Protection against repeated resend attempts

---

## 📁 File & Media Handling

The backend supports controlled handling of uploaded content used by the learning platform.

Depending on the configured workflow, the application can integrate with external media services while keeping the application responsible for:

* Validation
* Authentication
* Authorization
* Upload lifecycle management
* Secure access control

The project also includes support for **YouTube private uploads** through OAuth-based integration.

---

## 🛡️ Security

Security is treated as part of the architecture rather than an afterthought.

Implemented protections include:

### Application Security

* Password hashing with bcrypt
* Session-based authentication
* Session regeneration
* Role-based authorization
* Ownership authorization
* Strict request validation
* Rate limiting
* CORS configuration
* Security headers
* Protected routes
* Secure webhook validation

### Payment Security

* Webhook signature validation
* Idempotency protection
* Payment state validation
* Input validation

### Request Security

The application validates incoming data before allowing it to reach business logic or persistence layers.

---

## 🧱 Architecture

The backend follows a modular architecture built around clear separation of responsibilities.

```text
Client
  │
  ▼
Express.js
  │
  ├── Authentication Middleware
  ├── Authorization Middleware
  ├── Validation Middleware
  ├── Rate Limiting
  ├── Security Middleware
  │
  ▼
Routes / Controllers
  │
  ▼
Business Logic / Services
  │
  ├── Authentication
  ├── Courses
  ├── Lessons
  ├── Enrollment
  ├── Payments
  ├── Email Verification
  └── Media / Upload Services
  │
  ▼
Data Models
  │
  ▼
MongoDB
```

External services can be integrated alongside the application layer:

```text
                ┌───────────────┐
                │    Client     │
                └───────┬───────┘
                        │
                        ▼
                ┌───────────────┐
                │  Express API  │
                └───────┬───────┘
                        │
        ┌───────────────┼────────────────┐
        │               │                │
        ▼               ▼                ▼
   MongoDB         Payment Service   Email Service
                                          │
                                          ▼
                                   Media / YouTube
```

---

## 🗂️ Main Domain Models

The application is organized around the following core entities:

```text
User
 │
 ├── Student
 │     └── Enrollment
 │            └── Course
 │                   └── Lesson
 │
 ├── Teacher
 │     └── Course
 │            └── Lesson
 │
 └── Admin

Course
  │
  ├── Lessons
  └── Enrollments

Payment
  │
  └── Enrollment / Course Access
```

This structure keeps relationships between users, courses, lessons, enrollments, and payments explicit.

---

## 🔌 API Design

The backend exposes REST-oriented endpoints for the major platform resources.

Typical API domains include:

```text
/auth
/users
/courses
/lessons
/enrollments
/payments
/uploads
```

Endpoints are protected according to:

* Authentication requirements
* User role
* Resource ownership
* Request validation
* Business rules

For security reasons, production credentials, secrets, webhook keys, and private service configuration are intentionally excluded from this public documentation.

---

## ✅ Validation

Validation is applied at the API boundary before data is processed by the application.

The validation layer covers areas such as:

* Request body validation
* Query parameters
* URL parameters
* Authentication payloads
* Course data
* Lesson data
* Payment requests
* Upload-related inputs

The goal is to reject malformed or unsafe input as early as possible.

---

## 🧪 Testing

The project includes automated tests covering important security and business-critical behavior.

The test suite currently covers areas including:

* Authentication
* Session handling
* Authorization
* Role-based access
* Ownership checks
* Payment validation
* Payment webhook verification
* Idempotency
* Rate limiting
* Request validation
* Security headers
* CORS behavior
* Media / upload workflows

The project also maintains regression-oriented checks to help ensure that security fixes and architectural changes do not introduce new failures.

> Test results and exact environment-specific execution details may change as the project evolves.

---

## 🛠️ Technology Stack

### Backend

* **Node.js**
* **Express.js**
* REST APIs

### Database

* **MongoDB**
* **Mongoose**

### Authentication & Security

* Passport.js
* Express Session
* Mongo-backed sessions
* bcrypt
* CORS
* Security headers
* Rate limiting

### External Services

* Resend
* Fawry
* YouTube API / OAuth

### Development & Testing

* JavaScript
* Git
* Postman
* Automated regression testing

---

## ⚙️ Environment Variables

The application uses environment variables for sensitive configuration.

A typical setup may include values for:

```env
NODE_ENV=
PORT=

MONGO_URI=
SESSION_SECRET=

RESEND_API_KEY=

FAWRY_*
YOUTUBE_*
```

> Never commit real credentials, API keys, session secrets, OAuth secrets, payment secrets, or production database credentials to Git.

For a public portfolio/demo version, use a sanitized `.env.example` containing variable names only.

---

## 🧑‍💻 Local Development

Because the production repository is private, the exact deployment configuration and private credentials are intentionally not published here.

A typical development workflow is:

```bash
# Clone the repository
git clone <private-repository-url>

# Enter the project
cd online-learning-platform

# Install dependencies
npm install

# Configure environment variables
# Create your local .env file

# Start the development server
npm run dev
```

Available scripts may vary as the project evolves.

---

## 🔄 Typical Request Flow

A protected API request generally follows this lifecycle:

```text
HTTP Request
     │
     ▼
Security Middleware
     │
     ▼
Rate Limiting
     │
     ▼
Authentication
     │
     ▼
Authorization
     │
     ▼
Validation
     │
     ▼
Controller / Service
     │
     ▼
Database / External Service
     │
     ▼
Validated Response
```

This layered flow helps keep authentication, authorization, validation, and business logic separated.

---

## 🎯 Engineering Priorities

The project is being developed with emphasis on:

**Security**
Protect authentication, sessions, payments, user data, and private resources.

**Maintainability**
Keep responsibilities separated and make future changes easier to reason about.

**Reliability**
Use validation and regression tests to reduce unexpected behavior.

**Scalability**
Keep the architecture modular enough to allow future expansion of platform features.

**Real-world usability**
Design the backend around an actual learning platform rather than a simple CRUD demonstration.

---

## 📈 Future Improvements

Potential areas for future development include:

* More comprehensive integration and end-to-end testing
* Background job processing
* Caching and performance optimization
* Observability and structured logging
* Expanded analytics
* Improved media processing
* CI/CD automation
* Containerized deployment
* More granular permissions
* Production monitoring

---

## 📌 Project Status

**Status:** 🚧 Active Development

This project is being developed toward real-world deployment, so the architecture and feature set may continue to evolve.

---

## 🔒 Repository & Security Notice

The production source code is intentionally kept private.

This public documentation exists to demonstrate:

* Backend architecture
* API design
* Authentication and authorization
* Database modeling
* Security practices
* Payment integration
* Testing strategy
* Engineering decisions

No production credentials or sensitive configuration should be exposed through this repository or its documentation.

---

## 👨‍💻 Author

**Ziad Teama**

AI Student · Aspiring ML Engineer

Interested in **AI/ML, Backend Engineering, and building production-oriented systems**.

[GitHub](https://github.com/ziadTeama-dev) · [LinkedIn](https://www.linkedin.com/in/ziad-teama-62a563378/)

---

<div align="center">

**Built to learn. Engineered to scale. 🚀**

</div>
