# Cloud Enabled Deployment In Action with GCP

## Student Details
- Name: Ramesh Layan
- StudentId: 2301671065
- email: rameshlayan4@gmail.com

This repository contains my **Practical Assignment** for connecting a **MySQL database hosted on Google Cloud Platform (GCP)** with a microservices-based application and a React frontend.

---

This repository contains four projects:

- course-service (Spring Boot + MySQL)
- student-service (Spring Boot + MongoDB)
- media-service (Spring Boot + Local file storage, can be extended to S3/MinIO)
- frontend-app (React + TypeScript)

## Backend Services

### 1. course-service
- Entity: Course(id, name, duration)
- Endpoints:
  - GET /courses
  - GET /courses/{id}
  - POST /courses
  - DELETE /courses/{id}
- Default port: 8081
- Configure MySQL settings

### 2. student-service
- Document: Student(registrationNumber, fullName, address, contact, email)
- Endpoints:
  - GET /students
  - GET /students/{id}
  - POST /students
  - DELETE /students/{id}
- Default port: 8082
- Configure MongoDB settings

### 3. media-service
- Resource: files
- Endpoints:
  - POST /files (multipart/form-data: file)
  - GET /files (list)
  - GET /files/{id} (fetch)
  - DELETE /files/{id} (delete)
- Default port: 8083
- Uses local disk storage at `./data/media` by default (override with env var `MEDIA_STORAGE_DIR`).

## Frontend (frontend-app)
- React + TypeScript + MUI + Axios + Vite app with 3 sections: Courses, Students, Media
- Scripts:
  - npm run dev (Vite dev server)
  - npm run build (TypeScript build + Vite build)
  - npm run preview (Preview built app)

## Build

- Backend: run `mvn -q -e -DskipTests package` at repo root to build services.
- Frontend: run `npm install` then `npm run dev` inside `frontend-app`.

---

## Database Setup (MySQL on GCP)

1.Create a MySQL instance on GCP.

2.Note the following details:
- Host (Public IP or Connection Name)
- Port (default: 3306)
- Database Name
- Username & Password

3.Update each microservice with these credentials inside

- course-service/src/main/resources/application.properties
```properties
spring.application.name=course-service
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
server.port=8081
spring.profiles.active=gcp
```

- course-service/src/main/resources/application-gcp.properties
```properties
spring.datasource.url=jdbc:mysql://<GCP_HOST>:3306/<DB_NAME>
spring.datasource.username=<USERNAME>
spring.datasource.password=<PASSWORD>
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQLDialect
```

---
## Running the Microservices
- cd course-services
- mvn spring-boot:run

- cd ../media-services
- mvn spring-boot:run

- cd ../student-services
- mvn spring-boot:run

## Video Demonstration
[Video_ref](https://drive.google.com/file/d/1ms0J9A8xz61TLLkVaDNvnWWhsBaI47JE/view?usp=sharing)
