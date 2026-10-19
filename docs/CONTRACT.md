# CONTRACT.md

## Overview

A private, web-based Kanban board for a business owner to manage tasks across their employees. Each task is tagged with one employee's name and lives in one of three columns: To Do, In Progress, Done. Access requires a login; the owner sees everything, employees see only their own tasks.

## Assumptions

- The owner is a single admin account created at setup time (no self-registration).
- Employees are created by the owner; they cannot create their own accounts.
- No email or notifications are required at this stage.
- A task belongs to exactly one employee and can be reassigned by the owner.
- The app is a single-page application served from the same origin as the API.

## Stack

| Layer | Choice | Version |
|-------|--------|---------|
| Runtime | Node.js | 20.11.0 |
| Framework | Express | 4.18.2 |
| Frontend | React | 18.2.0 |
| Bundler | Vite | 5.2.0 |
| Database | SQLite via better-sqlite3 | 9.4.3 |
| Auth | express-session + bcryptjs | 1.0.6 / 2.4.3 |
| Testing | Vitest | 1.4.0 |
| E2E | Playwright | 1.42.1 |

## Data model

### users
| Field | Type | Notes |
|-------|------|-------|
| id | INTEGER PK | auto-increment |
| name | TEXT | unique, shown as tag |
| password_hash | TEXT | bcrypt |
| role | TEXT | 'owner' or 'employee' |

### tasks
| Field | Type | Notes |
|-------|------|-------|
| id | INTEGER PK | auto-increment |
| title | TEXT | required |
| description | TEXT | optional |
| column | TEXT | 'todo', 'inprogress', 'done' |
| assignee_id | INTEGER FK | references users.id |
| created_at | TEXT | ISO-8601 |

## API contracts

See `docs/openapi.yaml` for full shapes.

| Method | Path | Who | What |
|--------|------|-----|------|
| POST | /api/auth/login | anyone | log in |
| POST | /api/auth/logout | logged in | log out |
| GET | /api/me | logged in | current user info |
| GET | /api/tasks | logged in | all tasks (owner) or own tasks (employee) |
| POST | /api/tasks | owner | create task |
| PATCH | /api/tasks/:id | owner or assignee | move or edit task |
| DELETE | /api/tasks/:id | owner | delete task |
| GET | /api/users | owner | list employees |
| POST | /api/users | owner | create employee |
| DELETE | /api/users/:id | owner | remove employee |

## Design tokens

```css
--color-bg: #f4f5f7;
--color-surface: #ffffff;
--color-primary: #0052cc;
--color-primary-text: #ffffff;
--color-text: #172b4d;
--color-text-muted: #5e6c84;
--color-border: #dfe1e6;
--color-todo: #e3fcef;
--color-inprogress: #fff7d6;
--color-done: #deebff;
--font-family: 'Inter', sans-serif;
--font-size-base: 16px;
--spacing-unit: 8px;
--radius: 4px;
```

All foreground/background pairs meet WCAG AA (4.5:1).

## Folder layout

```
/
├── server/
│   ├── index.js          # Express entry point
│   ├── db.js             # SQLite setup and migrations
│   ├── auth.js           # login/logout/session middleware
│   ├── routes/
│   │   ├── tasks.js      # task CRUD routes
│   │   └── users.js      # user management routes
│   └── seed.js           # creates default owner account
├── client/
│   ├── index.html
│   ├── main.jsx          # React entry
│   ├── App.jsx           # router + auth context
│   ├── pages/
│   │   ├── LoginPage.jsx
│   │   └── BoardPage.jsx
│   └── components/
│       ├── Column.jsx
│       ├── TaskCard.jsx
│       ├── TaskModal.jsx
│       └── UserBadge.jsx
├── tests/
│   ├── api/              # Vitest API tests
│   └── e2e/              # Playwright E2E tests
├── docs/
├── package.json
└── vite.config.js
```

## Requirement map

| Requirement | Task(s) |
|-------------|---------|
| BR-01 | Task 3 |
| BR-02 | Task 4 |
| BR-03 | Task 4 |
| BR-04 | Task 4 |
| BR-05 | Task 3, Task 4 |
| BR-06 | Task 3, Task 4 |
| BR-07 | Task 3 |
| BR-08 | Task 2 |
| BR-09 | Task 2 |
| BR-10 | Task 1, Task 3 |
| NFR-01 | Task 1 |
| NFR-02 | Task 4, Task 5 |
| NFR-03 | Task 2 |
| NFR-04 | Task 2 |
| NFR-05 | Task 4, Task 5 |
