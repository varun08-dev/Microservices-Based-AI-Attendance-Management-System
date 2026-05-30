# Microservices-Based-AI-Attendance-Management-System


# 1. Introduction

The AI-Powered Smart Attendance System is a microservices-based attendance management platform that automates attendance marking using facial recognition and liveness detection.

The system uses:

* Spring Boot for backend services
* FastAPI for AI processing
* OpenCV for face recognition
* MediaPipe for liveness detection
* JWT authentication for security

---

# 2. System Architecture

The project follows a microservices architecture consisting of:

## Auth Service

Handles:

* User authentication
* JWT generation
* Role management
* Authorization

Runs on:

* Port 8081

## Attendance Service

Handles:

* Attendance records
* Student management
* Attendance analytics
* Reports
* Unknown face logs

Runs on:

* Port 8082

## AI Recognition Service

Handles:

* Face recognition
* Liveness detection
* Face registration
* Model retraining

Runs on:

* Port 8000


## Services

| Service | Description |
|---|---|
| [Auth Service](https://github.com/varun08-dev/Attendance-AuthService) | JWT Authentication & RBAC |
| [Attendance Service](https://github.com/varun08-dev/Attendance-AttendanceService) | Attendance APIs & Analytics |
| [AI Recognition Service](https://github.com/varun08-dev/Attendance-AI-Recognition-Service) | Face Recognition & Liveness Detection |


---

# 3. Technologies Used

## Backend

* Java
* Spring Boot
* Spring Security
* Hibernate/JPA
* MySQL

## AI Service

* Python
* FastAPI
* OpenCV
* MediaPipe
* NumPy

## Tools

* Swagger
* Postman
* GitHub

---

# 4. Features

* AI-based attendance marking
* Face registration system
* Eye-blink liveness detection
* JWT authentication
* Role-based access control
* Daily attendance reports
* Attendance percentage tracking
* Unknown face detection
* Student management
* Analytics APIs

---

# 5. Attendance Workflow

1. Webcam captures student face
2. AI Service detects face
3. Liveness detection validates blink
4. Face recognition identifies student
5. Attendance request sent to Attendance Service
6. Attendance stored in database
7. Reports and analytics generated

---

# 6. Security

Implemented using:

* Spring Security
* JWT Authentication
* Protected APIs
* Role-based authorization

Roles:

* ADMIN
* TEACHER
* STUDENT

---

# 7. API Overview

## Attendance APIs

* POST /attendance/mark
* GET /attendance/student/{id}
* GET /attendance/student/{id}/percentage

## Report APIs

* GET /attendance/report/today
* GET /attendance/report/between

## Recognition APIs

* POST /attendance/log
* GET /attendance/log/unknown

---

# 8. Future Improvements

* Docker containerization
* API Gateway
* Redis caching
* Cloud deployment
* Real-time dashboard
* Multi-camera support
* Notification system

---

# 9. Conclusion

The project demonstrates the implementation of AI-powered attendance automation using microservices architecture, secure authentication, and computer vision technologies.
