Technical Design Document (TDD)

1. Introduction

1.1 Purpose

This document describes the technical architecture, software components, database design, REST API structure, and implementation strategy for UniEnroll, a Course Registration System.

1.2 Technology Stack

- Frontend: React and TypeScript
- Backend: FastAPI and Python
- Database: SQLite for MVP local development
- Data Communication: REST APIs and JSON
- Version Control: Git and GitHub
- API Testing: FastAPI Swagger UI
- Beta Database: PostgreSQL may be used for deployment.

2. System Architecture

The system follows a three-layer architecture.

2.1 Presentation Layer

The React frontend provides the user interface for browsing courses, viewing course details, and managing registrations. TypeScript provides static type checking.

2.2 Application Layer

FastAPI handles HTTP requests, validates incoming data, applies business rules, communicates with the database, and returns JSON responses.

2.3 Data Layer

The relational database stores course information, student records, user accounts, and registration records.

2.4 Data Flow

1. A user interacts with the React interface.
2. The frontend sends an HTTP request to the FastAPI backend.
3. FastAPI validates the request and executes the required business logic.
4. The backend reads or updates the database.
5. FastAPI returns a JSON response.
6. The frontend displays the result.

3. Proposed Project Structure

unienroll/
├── frontend/
│   ├── src/
│   │   ├── components/
│   │   ├── pages/
│   │   ├── services/
│   │   ├── types/
│   │   ├── App.tsx
│   │   └── main.tsx
│   ├── package.json
│   └── tsconfig.json
├── backend/
│   ├── app/
│   │   ├── routers/
│   │   ├── schemas/
│   │   ├── models/
│   │   ├── services/
│   │   ├── database.py
│   │   └── main.py
│   └── requirements.txt
├── docs/
│   ├── PRD.md
│   ├── SRS.md
│   └── TDD.md
├── .gitignore
└── README.md

4. Database Design

4.1 Student

Field| Description
id| Primary key
student_id| Unique student identifier
name| Student name
email| Student email

4.2 Course

Field| Description
id| Primary key
code| Unique course code
title| Course title
description| Course description
credits| Course credit value
prerequisites| Prerequisite information
capacity| Maximum enrollment, when applicable

4.3 Registration

Field| Description
id| Primary key
student_id| Foreign key referencing Student
course_id| Foreign key referencing Course
status| Registration status
created_at| Registration timestamp

A unique constraint on the combination of student and course identifiers shall prevent duplicate registrations.

4.4 Beta Data Model

The Beta release shall introduce a User entity containing account credentials and role information. Authentication identities should be linked to student profiles where appropriate.

5. REST API Design

Base URL for local development: "http://localhost:8000"

5.1 Course APIs

Method| Endpoint| Purpose
GET| "/courses"| List courses
GET| "/courses/{course_id}"| Retrieve course details
POST| "/courses"| Create a course
PUT| "/courses/{course_id}"| Update a course
DELETE| "/courses/{course_id}"| Delete a course

5.2 Registration APIs

Method| Endpoint| Purpose
POST| "/registrations"| Create a registration
GET| "/registrations"| List registration records
GET| "/registrations/{registration_id}"| Retrieve a registration
DELETE| "/registrations/{registration_id}"| Delete a registration

For MVP, the registration request will identify the student and course. These endpoints are for local project demonstration and shall not be considered secure for public deployment without authentication and authorization.

5.3 Beta APIs

Method| Endpoint| Purpose
POST| "/auth/login"| Authenticate a user
GET| "/auth/me"| Retrieve the current user
GET| "/students/me"| Retrieve the current student's profile
GET| "/students/me/registrations"| View the student's registrations
DELETE| "/registrations/{registration_id}"| Drop an authorized registration

All protected Beta endpoints shall enforce authentication and server-side permissions.

6. Request and Response Handling

The backend shall use Pydantic schemas to validate incoming request data and structure API responses.

Common HTTP status codes:

- "200 OK": Successful retrieval or update.
- "201 Created": Resource created successfully.
- "204 No Content": Resource deleted successfully.
- "400 Bad Request": Invalid operation or business rule violation.
- "401 Unauthorized": Authentication required or invalid credentials.
- "403 Forbidden": Insufficient permissions.
- "404 Not Found": Requested resource does not exist.
- "409 Conflict": Duplicate registration or conflicting data.
- "422 Unprocessable Entity": Request validation failed.

7. Security Design

MVP

- Validate incoming request data.
- Use database constraints to maintain data integrity.
- Keep secrets and local database files out of version control.
- Run the application locally for demonstration.

Beta

- Hash passwords using a suitable password-hashing algorithm.
- Implement secure authentication and role-based authorization.
- Enforce permissions on the backend rather than relying on frontend visibility.
- Restrict students to their own profile and registration records.
- Configure CORS for approved frontend origins.
- Use HTTPS and secure secret management in deployment.

8. Error Handling

The backend shall return consistent error responses for invalid input, missing resources, and registration conflicts. The frontend shall display understandable error messages instead of failing silently.

9. Testing Strategy

MVP Testing

- Test course CRUD endpoints.
- Test valid and invalid registration requests.
- Test duplicate registration prevention.
- Test database relationships and constraints.
- Verify frontend-to-backend communication.

Beta Testing

- Test login and logout.
- Verify student and administrator permissions.
- Test unauthorized access attempts.
- Test course capacity, prerequisites, and credit limits.
- Test deployment configuration and production API connectivity.

10. Implementation Plan

MVP Phase

1. Set up the React and TypeScript frontend.
2. Set up FastAPI and the database.
3. Implement course management APIs.
4. Implement registration APIs and validation.
5. Connect the frontend to the backend.
6. Test and demonstrate the application locally.

Beta Phase

1. Implement authentication.
2. Add role-based access control.
3. Build the student dashboard.
4. Implement course add/drop and advanced validation.
5. Strengthen security and automated testing.
6. Deploy and test the application.

11. Design Limitations

The initial architecture is intended for an academic demonstration. Features such as real-time seat locking, university ERP integration, large-scale concurrency handling, and timetable optimization are outside the initial scope.
