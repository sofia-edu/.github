


# API Requirements Documentation

## Authentication and User Management

### Login API
- **Endpoint:** `/auth/login`
- **Method:** POST
- **Payload:**
  - `email` (string, required)
  - `password` (string, required)

### Forgot Password API
- **Endpoint:** `/auth/forgot-password`
- **Method:** POST
- **Payload:**
  - `email` (string, required)

### Change Password API
- **Endpoint:** `/auth/change-password`
- **Method:** POST
- **Payload:**
  - `oldPassword` (string, required)
  - `newPassword` (string, required)

### Register API
- **Endpoint:** `/auth/register`
- **Method:** POST
- **Payload:**
  - Details of the entity representative looking to register

## Payment Integration

### Stripe API Integration
- **Endpoint:** `/payments/stripe`
- **Method:** POST
- **Payload:** Transaction details

## Department Management

### CRUD API for Departments
- **Endpoint:** `/departments`
- **Methods:** GET, POST, PUT, DELETE
- **Payload:**
  - `name` (string, required)
  - `code` (string, required)
  - `description` (string)
  - `admin` (array of objects with `first_name`, `last_name`, and `email`)

### Create Department Lead API
- **Endpoint:** `/departments/{departmentId}/leads`
- **Method:** POST
- **Payload:**
  - `first_name` (string, required)
  - `last_name` (string, required)
  - `email` (string, required)

## Program Management

### CRUD API for Programs
- **Endpoint:** `/departments/{departmentId}/programs`
- **Methods:** GET, POST, PUT, DELETE
- **Payload:**
  - `name` (string, required)
  - `code` (string, required)
  - `description` (string)
  - `admin` (array of objects with `first_name`, `last_name`, and `email`)

### Create Program Lead API
- **Endpoint:** `/programs/{programId}/leads`
- **Method:** POST
- **Payload:**
  - `first_name` (string, required)
  - `last_name` (string, required)
  - `email` (string, required)

## Course Management

### CRUD API for Courses
- **Endpoint:** `/courses`
- **Methods:** GET, POST, PUT, DELETE
- **Payload:**
  - `name` (string, required)
  - `code` (string, required)
  - `description` (string)

### CRUD API for Assigning courses to programs
- **Endpoint:** `/assign-courses`
- **Methods:** GET, POST, PUT, DELETE
- **Payload:**
  - `name` (string, required)
  - `code` (string, required)
  - `description` (string)

## Instructor Management

### CRUD API for Instructors
- **Endpoint:** `/instructors`
- **Methods:** GET, POST, PUT, DELETE
- **Payload:**
  - `name` (string, required)
  - `email_id` (string, required)

### CRUD API for Instructor Details
- **Endpoint:** `/instructors/{instructorId}/details`
- **Methods:** GET, POST, PUT, DELETE
- **Payload:** Details including education, experience, skills, projects

### CRUD API for Instructor Availability
- **Endpoint:** `/instructors/{instructorId}/availability`
- **Methods:** GET, POST, PUT, DELETE
- **Payload:** Availability slots

### Get Available Hours for Instructor per Institution
- **Endpoint:** `/institutions/{institutionId}/instructors/{instructorId}/available-hours`
- **Method:** GET

## Additional APIs (Suggested)

### Role and Permissions Management
- **Endpoint:** `/roles`
- **Methods:** GET, POST, PUT, DELETE
- **Payload:** Role details

### File Uploads Management
- **Endpoint:** `/files`
- **Methods:** GET, POST, DELETE
- **Payload:** File data

### Academic Year and Semester Management
- **Endpoint:** `/academic-years`
- **Methods:** GET, POST, PUT, DELETE
- **Payload:** Academic year and semester details

---

## Timetable Management

### CRUD API for Academic Years
- **Endpoint:** `/academic-years`
- **Methods:** GET, POST, PUT, DELETE
- **Payload:**
  - `year` (string, required)
  - `description` (string)
  - `start` (date, required)
  - `end` (date, required)

### CRUD API for Semesters
- **Endpoint:** `/academic-years/{yearId}/semesters`
- **Methods:** GET, POST, PUT, DELETE
- **Payload:**
  - `title` (string, required)
  - `start` (date, required)
  - `end` (date, required)

### Generate Timetable API
- **Endpoint:** `/timetable/generate`
- **Method:** POST
- **Payload:**
  - `academicYearId` (string, required)
  - `semesterId` (string, required)

## Instructor Availability

### Update Instructor Availability API
- **Endpoint:** `/instructors/{instructorId}/availability`
- **Method:** PUT
- **Payload:**
  - `entityId` (string, required)
  - `availability` (array of objects with `day`, `from`, `to`)
- **Note:** Availability should be in 1-hour or 30-minute time frames. Enforce this rule in the API logic.

---

## High-Level System Architecture

Here is a high-level overview of the system architecture for the college timetable management and instructor availability system:

### Front-End Layer
- **User Interface:** Web application for students, instructors, and administrators to interact with the system.
- **Web Services:** RESTful services to communicate with the back-end.

### Application Layer
- **API Gateway:** A single entry point for all client requests, distributing them to appropriate services.
- **Authentication Service:** Manages user authentication and authorization.
- **Timetable Service:** Handles all operations related to timetable generation and management.
- **User Management Service:** Manages user accounts, roles, and permissions.
- **Department and Program Service:** Manages departments, programs, courses, and related entities.
- **Instructor Service:** Manages instructor details, including availability updates.

### Data Layer
- **Database Server:** A relational database that stores all application data in structured formats, as seen in the provided Draw.io diagram.
- **File Storage:** A file storage solution for uploading and storing documents and other files.

### Infrastructure Layer
- **Servers:** Hosts the back-end services and supports the application and data layers.
- **Load Balancer:** Distributes incoming network traffic across multiple servers to ensure reliability and availability.
- **Caching:** Improves response times and reduces database load by caching frequently accessed data.

### Integration Layer
- **Payment Processor Integration:** Connects with external services like Stripe for payment processing.
- **Email Service:** Sends emails for notifications, password resets, and other communications.

### Security Layer
- **Firewalls:** Protects the system from unauthorized access and potential threats.
- **Data Encryption:** Ensures that sensitive data is encrypted both at rest and in transit.

This architecture is designed to be modular and scalable, allowing each component to be developed, scaled, and maintained independently.

Remember, this is a simplified view and actual implementations may require more detail, such as choosing specific technologies, addressing cross-service communication, handling failover and redundancy, and ensuring compliance with data protection regulations.
