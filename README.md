🇵🇱 [Polish version](README_PL.md)

# Workforce Management System

A desktop application for managing employees, shift schedules, work time, tasks, and absences. Designed as a local application with a relational database and separate administrator and employee views.

---

## Features

- **Accounts and authentication:** individual accounts, `ADMIN` and `EMPLOYEE` roles, password changes and resets, account deactivation, and last login tracking.
- **Employee management:** contact details, employment dates and type, departments, positions, and active status. Deactivation preserves historical records.
- **Shift schedules:** reusable shift templates, assignments to employees on specific dates, weekly and monthly views, copying schedules, and conflict detection.
- **Work time tracking:** clocking in and out, comparing planned and actual hours, and administrator corrections.
- **Tasks:** assignments within an employee's scheduled shift, descriptions, priorities, statuses, estimated duration, and deadlines.
- **Task time tracking:** separate task sessions, allowing work on a task to be paused and resumed.
- **Absences:** administrator-managed vacation, sick leave, and other absences, with scheduling conflict checks.
- **Dashboards and reports:** employee, work time, task, and absence statistics for administrators; personal schedules, hours, and tasks for employees.
- **Audit log:** records of important account, employee, scheduling, and time tracking operations.

Planned schedules, actual work time, and task time are separate records. A shift template defines working hours, while a schedule entry assigns a shift to an employee on a specific date.

---

## Roles and Access

| Role | Access |
| --- | --- |
| `ADMIN` | Manage accounts, employees, departments, positions, shifts, schedules, tasks, and absences; correct work time entries and view reports across employees. |
| `EMPLOYEE` | View personal schedules and assigned tasks, record work and task time, and change their own password. |

Access checks are enforced in application logic. Passwords are stored as hashes. Validation prevents overlapping shifts, shifts during absences, duplicate active work sessions, and starting another employee's task or a task outside an active work session.

---

## Technology Stack

| Technology | Purpose |
| --- | --- |
| Python 3 | Application code |
| PySide6 | Desktop interface |
| SQLAlchemy 2.x | ORM and database access |
| SQLite | Local relational database |

---

## Project Structure

```text
workforce-management-system/
├── main.py
├── requirements.txt
├── README.md
├── README_PL.md
├── LICENCE
├── .gitignore
├── app/
│   ├── __init__.py
│   ├── database/             # Database configuration and initial data
│   │   ├── __init__.py
│   │   ├── database.py
│   │   └── seed.py
│   ├── models/               # ORM models
│   │   ├── __init__.py
│   │   ├── user.py
│   │   ├── employee.py
│   │   ├── department.py
│   │   ├── position.py
│   │   ├── shift.py
│   │   ├── schedule_entry.py
│   │   ├── work_time_entry.py
│   │   ├── task.py
│   │   ├── task_time_entry.py
│   │   ├── absence.py
│   │   └── audit_log.py
│   ├── logic/                # Authentication and business rules
│   ├── ui/
│   │   ├── __init__.py
│   │   ├── login_window.py
│   │   ├── main_window.py
│   │   ├── pages/            # Dashboards and module pages
│   │   ├── dialogs/          # Add and edit forms
│   │   └── widgets/          # Shared interface elements
│   ├── security/             # Password hashing and verification
│   ├── utils/                # Validation and date/time helpers
│   └── resources/
│       ├── icons/
│       │   └── icon.ico
│       └── styles/
│           └── main.qss
├── data/
│   └── .gitkeep
└── tests/
    ├── test_auth.py
    ├── test_work_time.py
    ├── test_schedules.py
    └── test_tasks.py
```

The data flow is **UI → business logic → SQLAlchemy models → SQLite**. Interface code calls functions in `app/logic/` to perform operations and validate business rules.

The local SQLite database is stored at `data/workforce.db`. Database files are excluded from version control.

---

## Future Improvements

---

## Requirements & Installation

### Python

Python 3.12 is recommended.

### Install dependencies

Install dependencies from `requirements.txt`:

```bash
pip install -r requirements.txt
```

### Run from source

```bash
python main.py
```

---

## Building the Windows Application

PyInstaller can be used to create the Windows application.

Example build command:

```bash
python -m pip install pyinstaller
python -m PyInstaller --windowed --icon="app/resources/icons/icon.ico" --name "Workforce Management System" --add-data "app/resources;app/resources" main.py
```

---

## Tests

The `tests/` directory groups tests for authentication and access restrictions, starting and finishing work, schedule conflicts and absences, and task ownership and time tracking.

---

## License

Copyright © 2026 Michał Rusek (Vyroxes), Kacper Kwiatek (vitalyi11), and Aleksandra Tworek (abelxoo). All rights reserved.

Except where otherwise noted, the source code is publicly available for
personal, non-commercial, and educational purposes only.

Commercial use, redistribution, sublicensing, and distribution of modified
versions are not permitted without prior written permission.

Third-party components remain subject to their respective licenses.

See [LICENCE](LICENCE) for the project license.

---

**Authors:**

- Michał Rusek (Vyroxes)
- Kacper Kwiatek (vitalyi11)
- Aleksandra Tworek (abelxoo)