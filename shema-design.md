## Overview

In this lab, you will design the data structure for the **Smart Clinic Management System** using both **MySQL (relational)** and **MongoDB (document-based)** databases.

Imagine you're a backend engineer starting with a clean slate. For designing the data structure for the Smart Clinic Management System,  ask yourself:  
- What kind of data should a smart clinic store? 
- How will we organize it? 
- Which data belongs in MySQL? Which in MongoDB?

### Key Tasks
In this lab, you'll create a markdown file to **document your schema ideas and design for both SQL and MongoDB databases**. You will need to refer to these designs for building your models and database logic.


## Learning Objectives

By the end of this lab, you will be able to:

- Analyze the data needs of a real-world application.
- Design SQL tables with appropriate columns, types, and relationships.
- Design MongoDB collections that support flexible data requirements.
- Decide what data belongs in structured SQL and what belongs in flexible NoSQL.
- Document your schema clearly for future development.


## Start with Real-World Thinking

Before jumping into tables and collections, think about what a smart clinic does.

Here are some real-world actions that a clinic management system should support:

- Registering patients and doctors
- Scheduling and tracking appointments
- Creating and managing prescriptions
- Managing doctor availability and working hours
- Storing notes or feedback
- Possibly even chat records, payment history, or uploadable documents

These needs give rise to **entities** (like Patient, Doctor, Appointment) and **relationships** (e.g., a Patient has many Appointments).


Next, go to your GitHub account and **open the repository you created from the template in the Create User Stories lab**:


java-database-capstone

In the **base directory** of your repository, create a new file named:

schema-design.md

You will add the following two sections in this file:
- MySQL Database Design
- MongoDB Collection Design


## MySQL Database Design – Think and Create

Structured, validated, and interrelated data works well in MySQL. Think of the core operational data for the clinic.

Create a section in your file titled:

## MySQL Database Design

### Instructions:

1. List at least **4 tables** that your clinic system needs.
   - Start with: patients, doctors, appointments, admin
   - Add others if needed: clinic_locations, payments

2. For each table:
   - Define **columns**
   - Specify **data types**
   - Mark **primary keys** and any **foreign key relationships**

3. Consider constraints:
   - Should some fields be NOT NULL, UNIQUE, or AUTO_INCREMENT
   - Should we validate email or phone formats later via code?

4. Ask yourself:
   - What happens if a patient is deleted? Should appointments also be deleted?
   - Should a doctor be allowed to have overlapping appointments?

### Example structure:

### Table: appointments
- id: INT, Primary Key, Auto Increment
- doctor_id: INT, Foreign Key → doctors(id)
- patient_id: INT, Foreign Key → patients(id)
- appointment_time: DATETIME, Not Null
- status: INT (0 = Scheduled, 1 = Completed, 2 = Cancelled)

Consider defining the structure of other tables in the format as per the given example. 

**Think deeper:**

- Should each doctor have their own available time slots?
- Should a patients past appointment history be retained forever?
- Is a prescription tied to a specific appointment or can it exist independently?

Write your design clearly and justify choices as comments in the file if needed.


## MongoDB Collection Design – Be Flexible

Some data doesn'fit well into rigid tables. For instance:

- Free-form doctor notes
- Optional patient feedback
- Prescription metadata
- File attachments
- Log records (when a patient checks in or messages a doctor)

These are great candidates for **MongoDB** – a flexible NoSQL database.

In the markdown file, create a section titled:

## MongoDB Collection Design

### Instructions:

1. Think of **one collection** that complements your MySQL schema.
   - Use prescriptions, feedback,logs, or messages.

2. Provide an **example document** using JSON syntax.

3. Be creative:
   - Add fields like tags, metadata, or nested structures.
   - Use arrays or embedded documents if they make sense.

### Example:

### Collection: prescriptions

```json
{
  "_id": "ObjectId('64abc123456')",
  "patientName": "John Smith",
  "appointmentId": 51,
  "medication": "Paracetamol",
  "dosage": "500mg",
  "doctorNotes": "Take 1 tablet every 6 hours.",
  "refillCount": 2,
  "pharmacy": {
    "name": "Walgreens SF",
    "location": "Market Street"
  }
}
**Think deeper:**

- Should MongoDB documents include the full patient object or just an ID?
- What would a chat message document look like?
- What happens if the schema needs to evolve – will your design support that?
