# Business Requirements: Employee Kanban Board

## Goal

A private Kanban board for a business owner to manage tasks across their employees. Each task is tagged with the employee's name so it is always clear who owns what. Only people with a login can access the board.

## Users

- **Owner (admin):** the business owner who creates tasks, assigns them to employees, and oversees all work.
- **Employees:** staff members who log in and manage their own assigned tasks.

## Business requirements

| ID | Requirement |
|----|-------------|
| BR-01 | The owner can create a new task with a title, description, and an employee tag (the employee's name). |
| BR-02 | The owner can see all tasks for all employees on one board. |
| BR-03 | The board has three columns: To Do, In Progress, and Done. |
| BR-04 | Each employee can log in and see a personal view that shows only tasks tagged with their name. |
| BR-05 | An employee can move their own tasks between columns (To Do → In Progress → Done). |
| BR-06 | The owner can move any task between columns. |
| BR-07 | The owner can edit or delete any task. |
| BR-08 | The owner can add or remove employee accounts. |
| BR-09 | Each employee account has a unique name that appears as a tag on their tasks. |
| BR-10 | A task can only be tagged to one employee at a time. |

## Quality requirements

- NFR-01: The board loads in under 2 seconds on a standard phone connection.
- NFR-02: The app works on both mobile phones and desktop browsers without loss of functionality.
- NFR-03: All pages are accessible only after login; no content is visible to unauthenticated visitors.
- NFR-04: Passwords are stored securely and never shown in plain text.
- NFR-05: The interface is readable and usable on small screens (minimum 320px wide).

## Not included

- No notifications or email alerts.
- No file attachments on tasks.
- No due dates or deadlines on tasks.
- No time tracking.
- No public or guest access to the board.
- No integration with external tools (Slack, email, etc.).

## Decisions

- **Columns:** To Do, In Progress, Done — the simplest set that covers most workflows.
- **Login:** each user (owner and employees) has their own account; login is required to access anything.
- **Task visibility:** the owner sees everything; each employee sees only tasks tagged with their own name.
- **Task assignment:** one task belongs to one employee; the owner assigns it at creation and can reassign later.
