# SOA_SKILL_EXP_3
# 🔐 User Registration System with Validation

A Spring Boot REST API that implements user registration and login with input validation, PostgreSQL database integration, duplicate-user detection, and secure password hashing using BCrypt.

## 📌 Experiment Details

- **Experiment No.:** 3
- **Experiment Name:** User Registration System with Validation
- **Course:** SOA Programming and Microservices
- **Academic Year:** 2026–2027

## 🎯 Objective

To develop a validated user registration system that stores user information in a PostgreSQL database, validates input fields, prevents duplicate accounts, and verifies login credentials securely.

## 🛠️ Technologies Used

- ☕ Java 21
- 🌱 Spring Boot 3.5.16
- 🌐 Spring Web
- 🗄️ Spring Data JPA
- 🐘 PostgreSQL
- 📦 Maven
- ✅ Jakarta Bean Validation
- 🔒 BCrypt Password Hashing
- 🚀 Postman
- 💻 Spring Tool Suite (STS)

## ✨ Features

### 1. User Registration
- Registers users through a REST API.
- Stores user details in PostgreSQL.
- Rejects duplicate usernames and email addresses.
- Validates required fields and email format.
- Enforces a minimum password length of eight characters.

### 2. User Login
- Authenticates users using their username or email.
- Compares submitted passwords against stored BCrypt hashes.
- Returns appropriate responses for successful and failed login attempts.
- Avoids exposing passwords in API responses.

### 3. Input Validation
- Rejects empty usernames.
- Rejects empty email addresses.
- Checks email format.
- Rejects empty passwords.
- Rejects passwords shorter than eight characters.

### 4. Error Handling
- Handles duplicate registration attempts.
- Returns HTTP `400 Bad Request` for validation failures.
- Returns HTTP `401 Unauthorized` for invalid login credentials.
- Returns HTTP `409 Conflict` for duplicate usernames or email addresses.

## 🏗️ System Architecture

```text
        Client / Postman
               |
               v
      Spring Boot REST API
               |
               v
        UserController
         /          \
        v            v
 Registration       Login
 Validation       Verification
        |            |
        v            v
      UserRepository
               |
               v
          Spring Data JPA
               |
               v
       PostgreSQL Database
```

## 📂 Project Structure

```text
user-registration/
├── src/
│   └── main/
│       ├── java/
│       │   └── com/
│       │       └── soa/
│       │           └── userregistration/
│       │               ├── UserRegistrationApplication.java
│       │               ├── User.java
│       │               ├── UserRepository.java
│       │               ├── UserController.java
│       │               └── LoginRequest.java
│       └── resources/
│           └── application.properties
├── pom.xml
└── README.md
```

## ⚙️ Database Configuration

Create a PostgreSQL database named:

```sql
CREATE DATABASE user_registration_db;
```

Configure `src/main/resources/application.properties`:

```properties
spring.application.name=user-registration
server.port=8086

spring.datasource.url=jdbc:postgresql://localhost:5432/user_registration_db
spring.datasource.username=postgres
spring.datasource.password=YOUR_POSTGRES_PASSWORD

spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.format_sql=true
```

Replace `YOUR_POSTGRES_PASSWORD` with your local PostgreSQL password.

Hibernate automatically creates or updates the `users` table based on the entity configuration.

## 🔗 API Endpoints

| Method | Endpoint | Description |
|---|---|---|
| POST | `/api/users/register` | Register a new user |
| POST | `/api/users/login` | Authenticate a user |

Base URL:

```text
http://localhost:8086
```

### 📝 1. Register a User

**Endpoint**

```text
POST http://localhost:8086/api/users/register
```

**Request Body**

```json
{
  "username": "jaswanth01",
  "email": "jaswanth01@example.com",
  "password": "SecurePass123"
}
```

**Expected Response — 201 Created**

```json
{
  "message": "User registered successfully"
}
```

### 🔑 2. Login with Username

**Endpoint**

```text
POST http://localhost:8086/api/users/login
```

**Request Body**

```json
{
  "usernameOrEmail": "jaswanth01",
  "password": "SecurePass123"
}
```

**Expected Response — 200 OK**

```json
{
  "message": "Login successful"
}
```

### 📧 3. Login with Email

**Request Body**

```json
{
  "usernameOrEmail": "jaswanth01@example.com",
  "password": "SecurePass123"
}
```

**Expected Response:** `200 OK`, provided the credentials match an existing account.

## 🧪 Testing Scenarios

| Test Case | Expected HTTP Status | Expected Result |
|---|---|---|
| Valid registration | `201 Created` | User registered |
| Duplicate username | `409 Conflict` | Registration rejected |
| Duplicate email | `409 Conflict` | Registration rejected |
| Invalid email format | `400 Bad Request` | Validation error |
| Missing username | `400 Bad Request` | Validation error |
| Empty password | `400 Bad Request` | Validation error |
| Password shorter than 8 characters | `400 Bad Request` | Validation error |
| Valid login | `200 OK` | Login successful |
| Invalid login credentials | `401 Unauthorized` | Login rejected |

## 🔒 Security Measures

- **BCrypt hashing:** Passwords are hashed before being stored in the database.
- **Input validation:** Invalid and incomplete data is rejected.
- **Unique constraints:** Duplicate usernames and email addresses are prevented.
- **Safe responses:** API responses do not return stored password hashes.
- **Credential verification:** Login uses BCrypt password matching instead of comparing plain-text passwords.

> **Note:** This experiment implements basic credential verification. It does not generate JWTs, maintain login sessions, or configure a complete Spring Security authentication system.

## ▶️ How to Run

1. Install Java 21, Maven, and PostgreSQL.
2. Create the `user_registration_db` database.
3. Configure the database credentials in `application.properties`.
4. Import the project into Spring Tool Suite.
5. Update the Maven project dependencies.
6. Run `UserRegistrationApplication.java` as a Spring Boot application.
7. Open Postman.
8. Test the registration and login endpoints using the request bodies above.

## 📚 Concepts Learned

- REST API development using Spring Boot.
- Entity mapping using Jakarta Persistence.
- Database operations using Spring Data JPA.
- PostgreSQL integration.
- Bean validation using Jakarta Validation.
- Password hashing with BCrypt.
- HTTP status codes and API error handling.
- Basic authentication and credential verification.
- API testing using Postman.

## ✅ Conclusion

The User Registration System with Validation demonstrates how to build a Spring Boot REST API with database persistence, input validation, duplicate-account prevention, secure password storage, and basic login verification.

The experiment provides a foundation for implementing more advanced authentication mechanisms, including token-based authentication and JWT security.
