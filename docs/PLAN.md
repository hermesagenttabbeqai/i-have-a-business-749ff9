# PLAN.md

## Task 1: Project setup — package.json, DB, and shared types

- assignee: claude
- requirements: BR-10, NFR-01
- files: package.json, vite.config.js, server/db.js, server/seed.js
- branch: feature/setup
- done when: `npm install` succeeds, SQLite DB initialises with both tables, and the seed script creates a default owner account with name "owner" and password "owner123".

## Task 2: Auth API and user management

- assignee: claude
- requirements: BR-08, BR-09, NFR-03, NFR-04
- files: server/index.js, server/auth.js, server/routes/users.js, tests/api/auth.test.js, tests/api/users.test.js
- branch: feature/auth-users
- done when: login, logout, and /api/me work correctly; owner can create and delete employee accounts; all API tests pass.

## Task 3: Tasks API

- assignee: devin
- requirements: BR-01, BR-05, BR-06, BR-07, BR-10
- files: server/routes/tasks.js, tests/api/tasks.test.js
- branch: feature/tasks-api
- done when: owner can create, edit, reassign and delete tasks; employees can move only their own tasks; GET /api/tasks returns all tasks for owner and only own tasks for employee; all API tests pass.

  Full context for Devin:
  - Stack: Node.js 20, Express 4.18.2, SQLite via better-sqlite3 9.4.3, Vitest 1.4.0.
  - DB schema is in server/db.js (tables: users, tasks — see docs/CONTRACT.md).
  - Session middleware is in server/auth.js; req.session.userId and req.session.role are set on login.
  - Implement server/routes/tasks.js with all routes from docs/openapi.yaml under /api/tasks.
  - Write tests in tests/api/tasks.test.js using Vitest. Tests must start an in-memory SQLite DB, not touch the real one.
  - Do not touch any file outside the files list.

## Task 4: React frontend — board and login

- assignee: claude
- requirements: BR-02, BR-03, BR-04, BR-05, BR-06, NFR-02, NFR-05
- files: client/index.html, client/main.jsx, client/App.jsx, client/pages/LoginPage.jsx, client/pages/BoardPage.jsx, client/components/Column.jsx, client/components/TaskCard.jsx, client/components/TaskModal.jsx, client/components/UserBadge.jsx
- branch: feature/frontend
- done when: the login page authenticates users; the board shows three columns with task cards tagged by employee name; owner sees all tasks; employee sees only their own; tasks can be moved between columns by dragging or a button; the app is responsive down to 320px.

## Task 5: End-to-end tests

- assignee: claude
- requirements: NFR-02, NFR-05
- files: tests/e2e/board.spec.js
- branch: feature/e2e
- done when: Playwright tests cover login as owner, creating a task, moving it to Done, logging out, logging in as employee, and verifying only own tasks are visible; all tests pass.
