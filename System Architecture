# System Architecture

# Overview

The AI-Powered Smart Attendance System follows a microservices architecture where authentication, attendance management, and AI recognition are separated into independent services.

This architecture improves:

* scalability
* maintainability
* security
* modularity

---

# Microservices

## 1. Auth Service (Port 8081)

Responsibilities:

* User Signup/Login
* JWT Token Generation
* Role-Based Authorization
* Authentication Validation

Technologies:

* Spring Boot
* Spring Security
* JWT

---

## 2. Attendance Service (Port 8082)

Responsibilities:

* Attendance Management
* Student Management
* Attendance Reports
* Unknown Face Logs
* Attendance Analytics

Technologies:

* Spring Boot
* JPA/Hibernate
* MySQL

---

## 3. AI Recognition Service (Port 8000)

Responsibilities:

* Face Recognition
* Liveness Detection
* Face Registration
* Model Retraining

Technologies:

* FastAPI
* OpenCV
* MediaPipe

---

# Authentication Flow

1. User logs in through Auth Service
2. JWT token is generated
3. Token sent with protected requests
4. Attendance Service validates token
5. Access granted based on roles

---

# Attendance Marking Flow

1. Webcam captures face
2. AI service processes image
3. Face recognition identifies student
4. Liveness detection validates blink
5. Attendance payload sent to Attendance Service
6. Attendance stored in database

---

# Unknown Face Detection Flow

1. Face detected
2. Confidence below threshold
3. AI Service sends unknown recognition log
4. Attendance Service stores log entry

---

# Database Design

## Attendance Table

Stores:

* studentId
* confidence
* liveness status
* attendance status
* timestamp

## Student Table

Stores:

* student details
* department
* class
* dataset path

## RecognitionLog Table

Stores:

* unknown face logs
* confidence
* device information
* timestamps

---

# Security Architecture

Implemented using:

* JWT Authentication
* Spring Security
* Role-Based Access Control

Roles:

* ADMIN
* TEACHER
* STUDENT

---

# Advantages of Architecture

* Independent service deployment
* Better scalability
* Easier maintenance
* Secure authentication flow
* AI service isolation
* Extensible design
