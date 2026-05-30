# API Documentation



---

# Base URLs

## Auth Service

```txt
http://localhost:8081
```

## Attendance Service

```txt
http://localhost:8082
```

## AI Recognition Service

```txt
http://localhost:8000
```

---

# Authentication

The system uses JWT-based authentication.

Protected APIs require:

```txt
Cookie: jwtToken  <JWT_TOKEN>
```

Roles:

* ADMIN
* TEACHER
* STUDENT

---

# 1. AUTH SERVICE APIs

---

# 1.1 User Signup

## Endpoint

```txt
POST /api/v1/auth/User/SignUp
```

## Description

Registers a new user into the system.

## Authorization

Public

## Request Body

```json
{
  "name": "Varun",
  "email": "varun@gmail.com",
  "password": "123456",
  "role": "STUDENT"
}
```

## Response

### Success Response

```json
{
  "message": "User registered successfully"
}
```

### Error Response

```json
{
  "message": "Email already exists"
}
```

---

# 1.2 User Login

## Endpoint

```txt
POST /api/v1/auth/User/Signin
```

## Description

Authenticates user and generates JWT token.

## Authorization

Public

## Request Body

```json
{
  "email": "varun@gmail.com",
  "password": "123456"
}
```

## Response

### Success Response

```json
{
  "jwtToken": "JWT_TOKEN"
}
```

### Error Response

```json
{
  "message": "Invalid credentials"
}
```

---

# 2. STUDENT MANAGEMENT APIs

---

# 2.1 Register Student

## Endpoint

```txt
POST /attendance/register
```

## Description

Registers a student in Attendance Service.

## Authorization

ADMIN only

## Request Body

```json
{
  "id": 101,
  "name": "Varun",
  "email": "varun@gmail.com",
  "className": "B.Tech",
  "department": "CSE",
  "datasetPath": "dataset/101"
}
```

## Success Response

```json
{
  "message": "Student registered successfully"
}
```

## Error Response

```json
{
  "message": "Student already exists"
}
```

---

# 2.2 Delete Student

## Endpoint

```txt
DELETE /attendance/delete/{studentId}
```

## Description

Deletes an existing student.

## Authorization

ADMIN only

## Path Variables

| Parameter | Type | Description |
| --------- | ---- | ----------- |
| studentId | Long | Student ID  |

## Success Response

```json
{
  "message": "Student deleted successfully"
}
```

---

# 3. ATTENDANCE APIs

---

# 3.1 Mark Attendance

## Endpoint

```txt
POST /attendance/mark
```

## Description

Marks attendance after successful face recognition and liveness detection.

## Authorization

AI Service

## Request Body

```json
{
  "studentId": 101,
  "confidence": 92.5,
  "livenessPassed": true,
  "deviceId": "CAMERA_01"
}
```

## Success Response

```json
{
  "success": true,
  "message": "Attendance marked successfully",
  "timestamp": "2026-05-30T10:30:00"
}
```

## Error Responses

### Low Confidence

```json
{
  "success": false,
  "message": "Low confidence face match",
  "timestamp": "2026-05-30T10:30:00"
}
```

### Liveness Failed

```json
{
  "success": false,
  "message": "Liveness detection failed",
  "timestamp": "2026-05-30T10:30:00"
}
```

### Duplicate Attendance

```json
{
  "success": false,
  "message": "Attendance already marked recently",
  "timestamp": "2026-05-30T10:30:00"
}
```

---

# 3.2 Get Student Attendance

## Endpoint

```txt
GET /attendance/student/{studentId}
```

## Description

Returns attendance history of a student.

## Authorization

* STUDENT
* TEACHER
* ADMIN

## Path Variables

| Parameter | Type | Description |
| --------- | ---- | ----------- |
| studentId | Long | Student ID  |

## Success Response

```json
[
  {
    "id": 1,
    "studentId": 101,
    "confidence": 92.5,
    "livenessPassed": true,
    "markedAt": "2026-05-30T10:30:00",
    "status": "PRESENT",
    "deviceId": "CAMERA_01"
  }
]
```

---

# 3.3 Get Attendance Percentage

## Endpoint

```txt
GET /attendance/student/{studentId}/percentage
```

## Description

Returns attendance percentage of student.

## Authorization

* STUDENT
* TEACHER
* ADMIN

## Path Variables

| Parameter | Type | Description |
| --------- | ---- | ----------- |
| studentId | Long | Student ID  |

## Success Response

```json
{
  "studentId": 101,
  "attendancePercentage": 92.5
}
```

---

# 3.4 Get Today's Attendance

## Endpoint

```txt
GET /attendance/student/today
```

## Description

Returns all attendance records marked today.

## Authorization

* TEACHER
* ADMIN

## Success Response

```json
[
  {
    "studentId": 101,
    "status": "PRESENT",
    "markedAt": "2026-05-30T10:30:00"
  }
]
```

---

# 3.5 Get Today's Absent Students

## Endpoint

```txt
GET /attendance/absent/today
```

## Description

Returns students who were absent today.

## Authorization

* TEACHER
* ADMIN

## Success Response

```json
[
  {
    "id": 102,
    "name": "Rahul",
    "department": "CSE"
  }
]
```

---

# 4. REPORT APIs

---

# 4.1 Daily Attendance Report

## Endpoint

```txt
GET /attendance/report/today
```

## Description

Returns today's attendance analytics.

## Authorization

* TEACHER
* ADMIN

## Success Response

```json
{
  "totalPresent": 52,
  "lateCount": 4,
  "recognizedStudents": 52,
  "studentIds": [101,102,103]
}
```

---

# 4.2 Attendance Report Between Dates

## Endpoint

```txt
GET /attendance/report/between
```

## Description

Returns attendance report between given dates.

## Authorization

* TEACHER
* ADMIN

## Query Parameters

| Parameter | Type      | Description |
| --------- | --------- | ----------- |
| startDate | LocalDate | Start Date  |
| endDate   | LocalDate | End Date    |

## Example

```txt
GET /attendance/report/between?startDate=2026-05-01&endDate=2026-05-30
```

## Success Response

```json
{
  "totalAttendance": 250,
  "recognizedStudents": 50
}
```

---

# 5. RECOGNITION APIs

---

# 5.1 Log Recognition Event

## Endpoint

```txt
POST /attendance/log
```

## Description

Stores unknown face recognition logs.

## Authorization

AI Service

## Request Body

```json
{
  "studentId": null,
  "confidence": 42,
  "livenessPassed": true,
  "recognitionStatus": "UNKNOWN_FACE",
  "deviceId": "CAMERA_01"
}
```

## Success Response

```json
{
  "message": "Recognition log stored"
}
```

---

# 5.2 Get Unknown Recognition Logs

## Endpoint

```txt
GET /attendance/log/unknown
```

## Description

Returns unknown face logs for a specific date.

## Authorization

ADMIN only

## Query Parameters

| Parameter | Type      | Description |
| --------- | --------- | ----------- |
| date      | LocalDate | Log Date    |

## Example

```txt
GET /attendance/log/unknown?date=2026-05-30
```

## Success Response

```json
[
  {
    "confidence": 42,
    "recognitionStatus": "UNKNOWN_FACE",
    "deviceId": "CAMERA_01"
  }
]
```

---

# 6. AI RECOGNITION SERVICE APIs

---

# 6.1 Register Face

## Endpoint

```txt
POST http://localhost:8000/register-face/{student_id}
```

## Description

Captures 30 face images and retrains recognition model.

## Path Variables

| Parameter  | Type    | Description |
| ---------- | ------- | ----------- |
| student_id | Integer | Student ID  |

## Process

1. Webcam starts
2. Face images captured
3. Images stored in dataset folder
4. LBPH model retrained
5. Trainer file updated

## Success Response

```json
{
  "message": "Face data for student 101 registered successfully"
}
```

---

# 6.2 Start Recognition

## Endpoint

```txt
GET http://localhost:8000/start-recognition
```

## Description

Starts face recognition and attendance marking process.

## Process

1. Detect face
2. Perform recognition
3. Perform liveness detection
4. Send attendance payload
5. Log unknown faces

## Success Response

```json
{
  "message": "Recognition stopped"
}
```

---

# 7. ERROR HANDLING

## Common HTTP Status Codes

| Code | Meaning               |
| ---- | --------------------- |
| 200  | Success               |
| 201  | Created               |
| 400  | Bad Request           |
| 401  | Unauthorized          |
| 403  | Forbidden             |
| 404  | Not Found             |
| 500  | Internal Server Error |

---

# 8. Swagger Documentation

Swagger UI:

```txt
http://localhost:8082/swagger-ui/index.html
```

---

# 9. Security Notes

* JWT tokens are required for protected APIs
* Role-based authorization implemented
* AI service communicates internally
* Admin endpoints protected using Spring Security

---

# 10. API Testing

Recommended Tools:

* Swagger UI
* Postman

Testing Flow:

1. Signup user
2. Login user
3. Copy JWT token
4. Authorize requests
5. Test APIs

---
