# Hospital Management - DevOps Project

## 1. Project overview
#### A simple hospital administration web app, with various features and different roles (i.e. patient, doctor, etc), each with their own privileges. The deliverable is a working DevOps pipeline, not necessarily the implementation of the application.
## 2. Requirement analysis
### 2.1 Functional requirements
#### FR-01: A receptionist should be able to register a new patient by entering the patient's basic information, including their name, date of birth, contact information, and address.
#### FR-02: Staff should be able to search for an existing patient and view their information when required
#### FR-03: Patient information should also be editable when circumstances change, for example when a patient changes their contact details.
#### FR-04: A patient record should also be possible to deactivate when it is no longer actively used, while preserving the information associated with previous appointments.
#### FR-05: An administrator should be able to register doctors in the system and record information such as their name, contact details, and medical specialization.
#### FR-06: Administrators should be able to view and update doctor information and deactivate doctors who are no longer available.
#### FR-07: The system should make it possible to identify which doctors are available to provide appointments and what specialization each doctor has.
#### FR-08: When creating an appointment, the receptionist should be able to select the patient and doctor and specify the date, time, and reason for the visit.
#### FR-09: An appointment should have a status indicating whether it is scheduled, completed, or cancelled.
#### FR-10: The application should prevent a doctor from being assigned two appointments at the same date and time.
#### FR-11: Hospital staff should be able to view existing appointments and update or cancel an appointment when necessary.
#### FR-12: Doctors should be able to access information about patients who have appointments with them.
#### FR-13: After an appointment, a doctor should be able to record basic information about the patient's visit, including the date of the visit, a diagnosis, and notes describing the outcome of the consultation.
#### FR-14: The application should retain these entries so that authorized medical staff can view the patient's previous records when required.
#### FR-15: The application should provide authentication so that users must log in before accessing protected functionality.
#### FR-16: The system should distinguish between receptionists, doctors, and administrators and should restrict functionality according to the user's role.
#### FR-17: For example, a receptionist should be able to manage patients and appointments but should not be able to modify a doctor's medical notes, while an administrator should be able to manage doctors and system users.
#### FR-18: A doctor should be able to access the appointments and medical information that they are authorized to view and export the data into a csv report.
### 2.2 Non-functional requirements
#### NFR-01: Normal application requests should normally be processed within two seconds when the system is operating under the expected demonstration workload.
#### NFR-02: The application should remain available during normal operation and should be capable of recovering automatically from an application or container failure in the deployment environment.
#### NFR-03: User passwords must not be stored in plain text
#### NFR-04: Users must be authenticated before accessing protected functionality.
#### NFR-05: A change on the main branch produces a published container image without manual steps.
#### NFR-06: Automated unit and end-to-end tests run in CI on every pull request.
#### NFR-07: Application and system metrics exposed and visible on a dashboard.
#### NFR-08: A documented branching strategy and a versioning scheme for artefacts.
## 3. Roles and access control
#### This application has three roles: Receptionist, Doctor, and Administrator. The Receptionist owns patient records and the appointment calendar. Registers, searches, edits and deactivates patients; schedules, updates and cancels appointments. Never touches clinical notes. Doctor sees the patients who have appointments with them. Records visit date, diagnosis and notes after a consultation, reads previous records, exports authorized data to CSV. Administrator manages the doctor register and system user accounts. Registers, updates and deactivates doctors; assigns roles. Not a clinical role. The patient is data, not a user. While there may be benefits to letting a patient be a role in cases (such as being able to log in to their account, book their own appointment, or read their own record), it is better to not give them these capabilities, as it may cause issues in the application and confusion between all the roles.
| Capability | Receptionist | Doctor | Administrator |
| :--- | :--- | :--- | :--- |
| Register, search and edit a patient | Yes | No | Yes |
| Deactivate a patient record | Yes | No | Yes |
| Register, update or deactivate a doctor | No | No | Yes |
| Schedule an appointment | Yes | Yes | Yes |
| View appointments | All | Own only | All |
| Update or cancel an appointment | Yes | Yes | Yes |
| Record diagnosis and visit notes | No | Yes | No |
| Read a patient's medical history | No | Own patients | No |
| Export authorised data to CSV | No | Yes | No |
| Manage user accounts and roles | No | No | Yes |
#### Administrators are not authorized to view patient data, so they should not be able to read or export patient's medical data. Doctors already have the patients' data, so it should be ok for them to schedule, update or cancel appointments.
## 4. Product backlog
#### US-20: As any staff member, I want to log in, so that I can reach only the functionality my role permits.
#### US-17: As an administrator, I want to create a user account and assign a role, so that users are aware of their privileges.
#### US-14: As an administrator, I want to register a doctor with a specialization, so that the hospital is aware of which services are offered.
#### US-01: As a receptionist, I want to register a new patient with their name, date of birth and contact details, so that the patient can be booked for an appointment.
#### US-05: As a receptionist, I want to schedule an appointment, so that the hospital stays organized and the doctor isn't double booked.
#### US-10: As a doctor, I want to record diagnosis and visit notes, so that the patient's data isn't forgotten or missed.
#### US-08: As a doctor, I want to view my scheduled appointments, so that I can plan my day accordingly and get ready for each patient.
#### US-07: As a receptionist, I want to view existing appointments, so that I can monitor the current schedule
#### US-02: As a receptionist, I want to search for an existing patient, so that useful patient info can be found.
#### US-09: As a doctor, I want to open the record of a patient I am seeing, so that I can be reminded on their information.
#### US-11: As a doctor, I want to Read a patient's previous records, so that I can see if the patient's history relates to current issues.
#### US-06: As a receptionist, I want to update or cancel an appointment, so that old/cancelled appointments don't overlap with another appointment.
#### US-03: As a receptionist, I want to edit patient contact details, so that the hospital can contact the patient.
#### US-15: As an administrator, I want to update doctor details, so that the hospital has up-to-date info.
#### US-19: As an administrator, I want to manage user accounts and roles, so that I can organize the hospital effectively.
#### US-13: As a doctor, I want to view other doctor specializations, so that I can coordinate referrals.
#### US-12: As a doctor, I want to export my authorized data to CSV, so that I can the complete picture of all of all my patients.
#### US-04: As a receptionist, I want to deactivate a patient record, so that a deactivated patient's data isn't stored without their consent.
#### US-16: As an administrator, I want to deactivate an unavailable doctor, so that appointments only happen with current, existing doctors.
#### US-18: As an administrator, I want to deactivate a user account, so that unavailable users' data isn't being stored without their consent.
#### I picked the top three because nothing can be demonstrated before login exists. Nothing books an appointment before patients and doctors exist.
#### US-20 — Login and Role-Based Access Control
#### • Given a receptionist user enters valid credentials on the login page, when they click "Log In", then they are authenticated and redirected to the receptionist dashboard.
#### • Given a doctor already has an appointment at 10:00 on 14 October, when a receptionist tries to book the same doctor at 10:00 on 14 October, then the system refuses and explains why
#### • Given an administrator is on the registration page, when they enter a doctor's name, contact details, and medical specialization and click "Register", then the doctor is added to the system and marked as available for appointments.
#### Definition of Done:
#### • Merged into main through a pull request, never pushed directly
#### • Unit tests written and passing in CI
#### • The end-to-end test for the affected flow is green
#### • The container image builds and is published to GHCR
#### • README updated if a requirement or decision changed

## 5. Process and ceremonies
#### Spring length - 2 weeks (4 sprints total)
#### 2 weeks is best because it makes sure I have time to do other schoolwork, while also keeping me on track to find on time.
#### • Sprint 1: Repo setup, branching strategy, Auth/RBAC, basic CI build/test pipeline.  
#### • Sprint 2: Patient & doctor CRUD, Docker containerization, publish pipeline.   
#### • Sprint 3: Scheduling with double-booking prevention, viewing medical notes, CSV export, CD deployment.   
#### • Sprint 4: Tests, monitoring/observability dashboard, double check README  docs.
#### Ceremonies
#### • Ceremony 1: When: Day 1 of the sprint (30–60 mins). What you do: Pick top backlog items and break them into tasks. What it produces: Sprint Backlog and Sprint Goal. 
#### • Ceremony 2: When: Last day of the sprint (30 mins). What you do: Demo working software to hypothetical user. What it produces: Feedback added to the backlog
#### • Ceremony 3: When: Right after Ceremony 2 (20 mins). What you do: Reflect on what went well and what didn't. What it produces: At least one actionable process change for the next sprint. 


**Epic 1: Authentication & User Management**

**User Story: US-20 — Login and Role-Based Access Control**
- **Story Points**: 8  
- **Description**: As any staff member, I want to log in, so that I can reach only the functionality my role permits.   
- **Dependencies**: None (Prerequisite for all other protected flows).   
- **Tasks**:
  - **Task 1.1**: Design and implement the database schema for users, roles (Receptionist, Doctor, Administrator), and password hashing (per NFR-03).   
  - **Task 1.2**: Implement backend authentication endpoints and role-based access control (RBAC) middleware.   
  - **Task 1.3**: Build the frontend login page with credential validation and role-based redirection.   
  - **Task 1.4 (Testing)**: Write automated unit tests for password hashing and RBAC permission checks, and an automated end-to-end (E2E) test verifying successful login and redirection to the appropriate dashboard.   

**User Story: US-17 — User Account & Role Creation**
- **Story Points**: 5 
- **Description**: As an administrator, I want to create a user account and assign a role, so that users are aware of their privileges.   
- **Dependencies**: Depends on US-20 (Authentication & RBAC framework).   
- **Tasks**:
  - **Task 1.7**: Implement backend API endpoints for administrators to create new user accounts and assign roles.   
  - **Task 1.8**: Build the administrator UI interface for user management and account creation.   
  - **Task 1.9 (Testing)**: Write automated unit tests for user creation constraints and an automated E2E test verifying that an administrator can successfully provision a new user account.   

**Epic 2: Patient Administration & Records**

**User Story: US-01 — Patient Registration**
- **Story Points**: 3 
- **Description**: As a receptionist, I want to register a new patient with their name, date of birth and contact details, so that the patient can be booked for an appointment.   
- **Dependencies**: Depends on US-20 (Receptionist login role verification).   
- **Tasks**:
  - **Task 2.1**: Create the database model and migration for patient records.   
  - **Task 2.2**: Implement backend CRUD endpoints for registering and validating patient data.   
  - **Task 2.3**: Build the receptionist dashboard form for patient registration.   
  - **Task 2.4 (Testing)**: Write automated unit tests for patient data validation rules and an automated E2E test for registering a new patient.   

**User Story: US-02 — Patient Search**
- **Story Points**: 3 
- **Description**: As a receptionist, I want to search for an existing patient, so that useful patient info can be found.   
- **Dependencies**: Depends on US-01 (Patient records must exist to search them).   
- **Tasks**:
  - **Task 2.5**: Implement backend search query endpoints (by name, identifier, or contact details).   
  - **Task 2.6**: Build the user interface component for searching and displaying patient search results.   
  - **Task 2.7 (Testing)**: Write automated unit tests for the search query logic and an automated E2E test verifying patient lookups.   

**User Story: US-03 — Edit Patient Details**
- **Story Points**: 2    
- **Description**: As a receptionist, I want to edit patient contact details, so that the hospital can contact the patient.   
- **Dependencies**: Depends on US-02 (Patient search/selection).   
- **Tasks**:
  - **Task 2.8**: Implement backend update endpoints for patient information.   
  - **Task 2.9**: Build the interface for editing existing patient profiles.   
  - **Task 2.10 (Testing)**: Write unit tests for update validation and an E2E test confirming modified details persist correctly.   

**User Story: US-04 — Deactivate Patient Record**
- **Story Points**: 3    
- **Description**: As a receptionist, I want to deactivate a patient record, so that a deactivated patient's data isn't stored without their consent.   
- **Dependencies**: Depends on US-02.   
- **Tasks**:
  - **Task 2.11**: Add soft-delete or deactivation flags to the patient database model and backend logic.   
  - **Task 2.12**: Add the deactivation control button/workflow in the patient management UI.   
  - **Task 2.13 (Testing)**: Write unit tests confirming past appointment data remains preserved while the profile is marked inactive, and an E2E test for the deactivation flow.   

**Epic 3: Doctor Registry & Management**

**User Story: US-14 — Doctor Registration**
- **Story Points**: 3    
- **Description**: As an administrator, I want to register a doctor with a specialization, so that the hospital is aware of which services are offered.   
- **Dependencies**: Depends on US-17 (Administrator user role).   
- **Tasks**:
  - **Task 3.1**: Create the database model and migrations for doctor profiles and specializations.   
  - **Task 3.2**: Implement backend endpoints to register doctors and assign specializations.   
  - **Task 3.3**: Build the administrator interface for registering doctors.   
  - **Task 3.4 (Testing)**: Write automated unit tests for doctor profile constraints and an automated E2E test verifying successful doctor registration.   

**User Story: US-15 — Update Doctor Details**
- **Story Points**: 2    
- **Description**: As an administrator, I want to update doctor details, so that the hospital has up-to-date info.   
- **Dependencies**: Depends on US-14.   
- **Tasks**:
  - **Task 3.5**: Implement backend update logic and endpoints for doctor information.   
  - **Task 3.6**: Create the UI views for editing doctor details.   
  - **Task 3.7 (Testing)**: Write unit and E2E tests for updating doctor attributes.   

**User Story: US-16 — Deactivate Doctor**
- **Story Points**: 3 
- **Description**: As an administrator, I want to deactivate an unavailable doctor, so that appointments only happen with current, existing doctors.   
- **Dependencies**: Depends on US-14.   
- **Tasks**:
  - **Task 3.8**: Implement backend deactivation logic checking for availability and scheduling rules.   
  - **Task 3.9**: Add UI triggers for doctor deactivation.   
  - **Task 3.10 (Testing)**: Write unit tests to ensure deactivated doctors cannot be selected for future appointments, backed by an E2E test.   

**User Story: US-13 — View Doctor Specializations**
- **Story Points**: 2    
- **Description**: As a doctor, I want to view other doctor specializations, so that I can coordinate referrals.   
- **Dependencies**: Depends on US-14 and US-20 (Doctor role).   
- **Tasks**:
  - **Task 3.11**: Implement backend read-only endpoints listing available doctors and specializations.   
  - **Task 3.12**: Build the directory component inside the doctor dashboard.   
  - **Task 3.13 (Testing)**: Write unit and E2E tests verifying doctors can view colleague specializations.   

**Epic 4: Appointment Scheduling & Workflow**

**User Story: US-05 — Schedule Appointment (with Double-Booking Prevention)**
- **Story Points**: 8    
- **Description**: As a receptionist, I want to schedule an appointment, so that the hospital stays organized and the doctor isn't double booked.   
- **Dependencies**: Depends on US-01 (Patients) and US-14 (Doctors).   
- **Tasks**:
  - **Task 4.1**: Create the database model and relational mapping for appointments (storing patient ID, doctor ID, date, time, status, and reason).   
  - **Task 4.2**: Implement business logic preventing a doctor from being assigned two overlapping appointments at the same date and time (per NFR rule / US-20 scenario).   
  - **Task 4.3**: Build the appointment booking UI form for receptionists.   
  - **Task 4.4 (Testing)**: Write automated unit tests for the double-booking conflict check logic, and an automated E2E test simulating a rejected double-booking attempt.   

**User Story: US-07 — View Appointments (Receptionist)**
- **Story Points**: 3    
- **Description**: As a receptionist, I want to view existing appointments, so that I can monitor the current schedule.   
- **Dependencies**: Depends on US-05.   
- **Tasks**:
  - **Task 4.5**: Implement backend endpoints to fetch all hospital appointments with filtering/sorting capabilities.   
  - **Task 4.6**: Build the full calendar/schedule view component for the receptionist dashboard.   
  - **Task 4.7 (Testing)**: Write unit and E2E tests validating that receptionists can see all appointments across the system.   

**User Story: US-06 — Update or Cancel Appointment**
- **Story Points**: 3    
- **Description**: As a receptionist, I want to update or cancel an appointment, so that old/cancelled appointments don't overlap with another appointment.   
- **Dependencies**: Depends on US-05.   
- **Tasks**:
  - **Task 4.8**: Implement backend update and cancellation status modification endpoints.   
  - **Task 4.9**: Build UI workflows for modifying or cancelling scheduled appointments.   
  - **Task 4.10 (Testing)**: Write unit tests for status changes (scheduled, completed, cancelled) and an E2E test for cancellation flows.   

**Epic 5: Clinical Notes, Medical History & Reporting**

**User Story: US-08 — View Scheduled Appointments (Doctor)**
- **Story Points**: 3    
- **Description**: As a doctor, I want to view my scheduled appointments, so that I can plan my day accordingly and get ready for each patient.   
- **Dependencies**: Depends on US-05 and US-20 (Doctor role).   
- **Tasks**:
  - **Task 5.1**: Implement scoped backend queries filtering appointments strictly by the logged-in doctor's ID.   
  - **Task 5.2**: Build the doctor's personal agenda/schedule dashboard view.   
  - **Task 5.3 (Testing)**: Write unit and E2E tests ensuring doctors can only see their own assigned appointments.   

**User Story: US-09 & US-11 — Open Patient Record & Read History**
- **Story Points**: 5    
- **Description**: As a doctor, I want to open the record of a patient I am seeing, so that I can be reminded of their information and read previous records.   
- **Dependencies**: Depends on US-08.   
- **Tasks**:
  - **Task 5.4**: Implement secure authorization checks ensuring doctors can only open records of patients they have active appointments with.   
  - **Task 5.5**: Build the doctor's patient chart view displaying demographic info and past visit histories.   
  - **Task 5.6 (Testing)**: Write unit tests for data access boundaries and an E2E test verifying authorized chart retrieval.   

**User Story: US-10 — Record Diagnosis and Visit Notes**
- **Story Points**: 3    
- **Description**: As a doctor, I want to record diagnosis and visit notes, so that the patient's data isn't forgotten or missed.   
- **Dependencies**: Depends on US-09.   
- **Tasks**:
  - **Task 5.7**: Create the database model and storage logic for consultation records (visit date, diagnosis, and notes).   
  - **Task 5.8**: Build the post-consultation data entry form on the doctor's interface.   
  - **Task 5.9 (Testing)**: Write unit tests for consultation entry persistence and an E2E test for recording a diagnosis.   

**User Story: US-12 — Export Authorized Data to CSV**
- **Story Points**: 5   
- **Description**: As a doctor, I want to export my authorized data to CSV, so that I can have the complete picture of all my patients.   
- **Dependencies**: Depends on US-10.   
- **Tasks**:
  - **Task 5.10**: Implement backend data-aggregation and CSV-generation service restricted to the doctor's own patient consultations.   
  - **Task 5.11**: Add the CSV download trigger button in the doctor dashboard.   
  - **Task 5.12**: Write automated unit tests verifying the structure and content of generated CSV reports, and an E2E test simulating a successful download.       
- **Description**: As any staff member, I want to log in, so that I can reach only the functionality my role permits. 
- **Tasks**:
  - **Task 1.1**: Design and implement the database schema for users, roles (Receptionist, Doctor, Administrator), and password hashing (per NFR-03).   
  - **Task 1.2**: Implement backend authentication endpoints and role-based access control (RBAC) middleware.   
  - **Task 1.3**: Build the frontend login page with credential validation and role-based redirection.   
  - **Task 1.4**: Write automated unit tests for password hashing and RBAC permission checks, and an automated end-to-end (E2E) test verifying successful login and redirection to the appropriate dashboard.   

**Sprint Duration**
- **Sprint Length**: **2 weeks** per sprint (total of **4 sprints** over an 8-week development lifecycle).   

**Sprint 1: Foundation, Authentication & CI Pipeline (Weeks 1–2)**
- **Sprint Goal**: Establish the repository infrastructure, versioning strategy, basic CI build/test pipeline, and core authentication framework.   
- **Backlog Items & Story Points**:
    - **US-20**: Login and Role-Based Access Control (8 Points)   
    - **US-17**: User Account & Role Creation (5 Points)   

**Sprint 2: Entity CRUD & Containerization (Weeks 3–4)**
- **Sprint Goal**: Implement comprehensive patient and doctor administration modules, package the application into a Docker container, and establish a container publishing pipeline.   
- **Backlog Items & Story Points**:
    - **US-01**: Patient Registration (3 Points)   
    - **US-02**: Patient Search (3 Points)   
    - **US-03**: Edit Patient Details (2 Points)   
    - **US-04**: Deactivate Patient Record (3 Points)   
    - **US-14**: Doctor Registration (3 Points)   
    - **US-15**: Update Doctor Details (2 Points)   
    - **US-16**: Deactivate Doctor (3 Points)   
    - **US-13**: View Doctor Specializations (2 Points)   

**Sprint 3: Core Scheduling, Clinical Notes & CD Deployment (Weeks 5–6)**
- **Sprint Goal**: Deliver the core appointment scheduling workflow with double-booking prevention, clinical note entry, patient history views, CSV data exporting, and CD deployment.   
- **Backlog Items & Story Points**:
    - **US-05**: Schedule Appointment with Double-Booking Prevention (8 Points)   
    - **US-07**: View Appointments - Receptionist (3 Points)   
    - **US-06**: Update or Cancel Appointment (3 Points)   
    - **US-08**: View Scheduled Appointments - Doctor (3 Points)   
    - **US-09 & 11**: Open Patient Record & Read History (5 Points)   
    - **US-10**: Record Diagnosis and Visit Notes (3 Points)   
    - **US-12**: Export Authorized Data to CSV (5 Points)   

**Sprint 4: Testing, Monitoring & Documentation Polish (Weeks 7–8)**
- **Sprint Goal**: Complete rigorous E2E testing coverage, implement application/system metrics dashboards for observability, and perform final documentation reviews.   
- **Backlog Items & Story Points**:
    - *Testing*: Comprehensive automated unit and end-to-end (E2E) test suites covering all user flows (per NFR-06).   
    - *Monitoring*: Expose application and system metrics on an operational dashboard (per NFR-07).   
    - *Documentation*: Double-check and update the `README.md` docs to ensure all requirements and architectural decisions match the final product.

**Tools (programming lanugages, frameworks, database, other services) used**
- **Backend**: Java & Spring Boot (with Spring Security for authentication and role-based access control).
- **Database**: PostgreSQL (for robust relational data management and transaction integrity).
- **Containerization**: Docker (to package the application for consistent local and production environments).
- **CI/CD Pipeline**: GitHub Actions (for automated testing on pull requests and automated image publishing to GHCR).
Observability: Spring Boot Actuator, Prometheus, and Grafana (for system metrics and operational dashboards).

**Branch Naming Convention**
``<issue-number>-<story-or-task-id>-<short-description>``

















