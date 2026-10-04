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
## 5. Process and ceremonies







