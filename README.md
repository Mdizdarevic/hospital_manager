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






























