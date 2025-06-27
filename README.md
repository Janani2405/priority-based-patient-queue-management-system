# 🏥 Healthcare Appointment and Triage Management System

A robust, smart healthcare queue and triage system built using **Flask** and **Oracle Database**, enabling role-based access, intelligent prioritization of appointments, and streamlined doctor-patient interaction.

---

## 🚀 Key Features

- ✅ Role-Based Access: Admin, Doctor, and Patient with separate dashboards
- 📋 Patient Registration with vitals, symptoms, and medical history
- 🩺 Intelligent Triage Classification (Critical, High, Low) based on inputs
- 📆 Doctor Scheduling with dynamic slot allocation per specialization
- 🔁 Emergency Queue with priority-based assignment
- 🧾 Prescription Upload and History Tracking (`PPD` table)
- 🔍 Real-Time Queue Monitoring with estimated wait times
- 📬 Email Notifications upon booking or updates
- 🔐 Secure Password Handling and Change Functionality

---

## 👥 Role-Based Workflow Overview

### 🧑‍⚕️ Doctor

- Logs in using a unique `USER_ID` and password
- Dashboard includes:
  - Appointments filtered by **date**, **time slot**, and **specialization**
  - Triage-prioritized queues
  - Patient vitals and symptoms
- Actions:
  - Mark patients as "Examined"
  - Add diagnosis & prescription (updates `PPD`)
  - View and manage their availability (via `DOCTOR_SCHEDULE`)
- Restrictions:
  - Maximum of **12 appointments per day**
  - Separate flows for regular, walk-in, and emergency patients

---

### 👤 Patient

- Registers/login via `USER_ID` and password
- Dashboard includes:
  - Book appointment by selecting a department/specialization
  - Input **vitals**, **symptoms**, and **history**
  - View **current queue position** and **estimated waiting time**
- Actions:
  - Reschedule (before 1-hour cutoff)
  - Cancel appointments
  - View appointment and diagnosis history
- Features:
  - Triage level calculated for **General Medicine** based on severity
  - Automatic time slot and doctor allocation

---

### 🛡️ Admin

- Logs in with special admin credentials
- Full control over:
  - **User Management** (View, Add, Delete doctors and patients)
  - **Doctor Scheduling** (Assign days/specializations)
  - **Toggle Availability** via the `DOCTORS` table
  - **Monitor** all queues: appointments, walk-ins, emergencies
- Also supports emergency doctor assignment and slot updates

---

## 🛠️ Tech Stack

| Layer      | Technology                        |
|------------|-----------------------------------|
| Backend    | Python 3.10+, Flask               |
| Frontend   | HTML, CSS, Jinja2                 |
| Database   | Oracle 19c with `pyodbc` connector |
| Mailing    | Gmail SMTP (via `smtplib`)        |
| Hosting    | Localhost (future: Render/Docker) |

---

## 📂 Project Structure

```

healthcare-system/
├── app.py                  # Main Flask application
├── templates/              # Jinja2 HTML templates
├── static/                 # CSS, JS, images
├── requirements.txt        # Python package dependencies
├── .env.example            # Sample environment config
├── .gitignore              # Git-ignored files/folders
├── README.md               # Project documentation
├── DEPLOYMENT.md           # SQL + setup steps
└── oracle\_tables.txt       # All Oracle DDL, triggers, sequences

````

---

## 🧾 Database Tables Overview

| Table Name        | Description                                 |
|-------------------|---------------------------------------------|
| `USERS1`          | All registered users: Patients, Doctors, Admins |
| `PATIENT_TRIAGE`  | Patient vitals, triage level, appointment info |
| `DOCTOR_SCHEDULE` | Doctors’ working days and specializations   |
| `DOCTORS`         | Availability status for doctors             |
| `PPD`             | Diagnosis, prescription, and consultation notes |
| `WALKINS`         | Walk-in patients assigned via token system  |
| `EMERGENCY_QUEUE` | Emergency appointments and quick routing    |

🧠 **Database Extras:**
- Oracle triggers for ID auto-generation
- Sequences for patient, doctor, and emergency IDs
- Constraints on roles, uniqueness, appointment limits

---

## 📦 Installation & Setup

### 🔧 Prerequisites

- Python 3.10+
- Oracle DB (local or cloud)
- `pyodbc` (configured with DSN for Oracle)
- Flask and required libraries

### 📥 Install Python Dependencies

```bash
pip install -r requirements.txt
````

### 🧱 Setup Database

Run the SQL script in your Oracle environment:

```
oracle_tables.txt
```

Ensure triggers, sequences, and constraints are created.

### ▶️ Start the Application

```bash
python app.py
```

Access via browser at:
`http://127.0.0.1:5000`

---

## 🧪 Sample Login Credentials

| Role    | User ID | Password | Description            |
| ------- | ------- | -------- | ---------------------- |
| Admin   | admin   | admin123 | Admin control panel    |
| Doctor  | D01     | cd01     | Cardiology             |
| Doctor  | D05     | gd05     | General Medicine       |
| Patient | P001    | p001     | Sample patient account |

---

## 🔄 GitHub Workflow

Keep your repo updated with:

```bash
git add .
git commit -m "Your message"
git push origin main
```

---

## 📌 Deployment Notes

* Store sensitive values (e.g., Gmail credentials) in `.env`
* Update your **Oracle DB connection** string in `app.py`
* Run all triggers and sequences before the app starts
* For email notifications, enable **App Passwords** in Gmail if 2FA is on

---

## ✨ Planned Enhancements

* Docker container with Oracle XE and Flask
* Role-based route protection (`@login_required`, etc.)
* Patient rescheduling interface with doctor suggestions
* Charts and visual reports for doctors (e.g., triage stats)

---

## 👩‍💻 Author

**Janani A.**
A software developer passionate about building life-improving applications with Python, data, and cloud technologies.

---

## ⭐ Support & Contributions

If you found this project helpful:

* ⭐ Star this repo to show support
* 🍴 Fork to build your version
* 🐛 Open issues for bugs/suggestions

---

````
