Product Requirements Document (PRD)

1. Project Overview

Project Name: UniEnroll — Course Registration System

Project Type: Web Application

Course: CSE309

UniEnroll is a university course registration web application designed to help students browse available courses, register for courses, and manage their registrations. Administrators can manage course information and monitor registration records.

2. Problem Statement

Managing course information and student registrations manually can be time-consuming and may lead to duplicate entries, inaccurate records, and difficulty tracking available courses. UniEnroll aims to organize these activities through a centralized web application.

3. Project Objectives

- Provide an organized course catalog.
- Allow students to register for available courses.
- Prevent duplicate course registrations.
- Enable administrators to manage courses.
- Maintain accurate registration records.
- Introduce secure authentication and role-based access in the Beta release.

4. Target Users

Students: Browse courses, view course details, register for courses, and manage their registrations.

Administrators: Create, view, update, and delete course records and monitor student registrations.

5. Functional Scope

Release 1: MVP (Midterm Demo)

- View the course catalog.
- View course details, credits, and prerequisites.
- Create, view, update, and delete course records.
- Create and view course registrations.
- Prevent duplicate registrations.
- Store and retrieve data from a database.
- Provide REST APIs that can be tested locally.

Release 2: Beta (Final Demo)

- User authentication and logout.
- Role-Based Access Control (RBAC).
- Student profile dashboard.
- Register for and drop courses.
- Validate seat availability and course prerequisites.
- Enforce credit limits and registration rules.
- Protect APIs with appropriate permissions.
- Deploy the application for demonstration.

6. Non-Functional Goals

- Usable and responsive interface.
- Maintainable and modular code.
- Reliable data storage and validation.
- Secure handling of credentials and permissions in Beta.
- Clear API documentation.

7. Technology Stack

- Frontend: React with TypeScript
- Backend: FastAPI with Python
- Database: SQLite for initial local development
- API Style: REST
- Version Control: Git and GitHub

8. Success Criteria

- Users can browse available courses.
- Course records can be managed through REST APIs.
- Valid registrations are saved successfully.
- Duplicate registrations are rejected.
- MVP runs locally and can be demonstrated.
- Beta features are implemented and tested before the final demo.

9. Out of Scope

The initial project does not include payment processing, university ERP integration, automatic timetable optimization, or mobile applications.

10. Risks and Limitations

Limited development time may affect the number of completed features. Therefore, MVP features will be prioritized, and advanced security, dashboard, and deployment features will be developed during Beta.
