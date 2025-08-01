# BETTER - EMS

## Tech Stack

* **Backend**: Node.js + Express
* **Auth**: JWT-based authentication
* **DB**: PostgreSQL or MongoDB
* **ORM**: Prisma

## API ROUTE STRUCTURE

### AUTH ROUTES (`/api/auth`)

| Method | Route         | Description                         | Access        |
| ------ | ------------- | ----------------------------------- | ------------- |
| POST   | `/register` | Register new user (student/faculty) | Public        |
| POST   | `/login`    | Login and get JWT                   | Public        |
| POST   | `/logout`   | Invalidate session                  | Authenticated |
| GET    | `/me`       | Get current user profile            | Authenticated |

---

### STUDENT ROUTES (`/api/students`)

| Method | Route         | Description                   | Access        |
| ------ | ------------- | ----------------------------- | ------------- |
| GET    | `/`         | Get all students (admin only) | Admin         |
| GET    | `/:roll_no` | Get specific student profile  | Student/Admin |
| PUT    | `/:roll_no` | Update student profile        | Student/Admin |
| DELETE | `/:roll_no` | Delete student                | Admin         |

---

### FACULTY ROUTES (`/api/faculty`)

| Method | Route            | Description            | Access |
| ------ | ---------------- | ---------------------- | ------ |
| GET    | `/`            | List all faculty       | Admin  |
| POST   | `/`            | Create new faculty     | Admin  |
| GET    | `/:faculty_id` | Get faculty by ID      | Public |
| PUT    | `/:faculty_id` | Update faculty details | Admin  |
| DELETE | `/:faculty_id` | Remove faculty         | Admin  |

---

### CLUB ROUTES (`/api/clubs`)

| Method | Route         | Description       | Access |
| ------ | ------------- | ----------------- | ------ |
| GET    | `/`         | List all clubs    | Public |
| GET    | `/:club_id` | Get club details  | Public |
| POST   | `/`         | Create a new club | Admin  |
| PUT    | `/:club_id` | Update club       | Admin  |
| DELETE | `/:club_id` | Delete club       | Admin  |

#### Club Membership (`/api/clubs/:club_id/members`)

| Method | Route         | Description                     | Access |
| ------ | ------------- | ------------------------------- | ------ |
| GET    | `/`         | List all members of the club    | Auth   |
| POST   | `/`         | Add student to club (with role) | Admin  |
| PUT    | `/:roll_no` | Update member role              | Admin  |
| DELETE | `/:roll_no` | Remove member from club         | Admin  |

---

### EVENT ROUTES (`/api/events`)

| Method | Route          | Description        | Access              |
| ------ | -------------- | ------------------ | ------------------- |
| GET    | `/`          | List all events    | Public              |
| POST   | `/`          | Create a new event | Admin/Club Convenor |
| GET    | `/:event_id` | Get event by ID    | Public              |
| PUT    | `/:event_id` | Update event       | Convenor/Admin      |
| DELETE | `/:event_id` | Delete event       | Admin               |

---

### TEAM ROUTES (`/api/teams`)

| Method | Route         | Description                   | Access       |
| ------ | ------------- | ----------------------------- | ------------ |
| GET    | `/`         | Get all teams                 | Admin        |
| POST   | `/`         | Create a team                 | Student      |
| GET    | `/:team_id` | Get team details              | Student      |
| PUT    | `/:team_id` | Update team name, is\_present | Leader       |
| DELETE | `/:team_id` | Disband team                  | Leader/Admin |

#### Team Members (`/api/teams/:team_id/members`)

| Method | Route         | Description                        | Access      |
| ------ | ------------- | ---------------------------------- | ----------- |
| GET    | `/`         | Get all members in the team        | Team        |
| POST   | `/`         | Add member (after invite accepted) | Team Leader |
| DELETE | `/:roll_no` | Remove member                      | Team Leader |

---

### INVITATION ROUTES (`/api/invitations`)

| Method | Route         | Description                      | Access      |
| ------ | ------------- | -------------------------------- | ----------- |
| POST   | `/`         | Send invite to a student         | Team Leader |
| GET    | `/incoming` | Get your incoming invites        | Student     |
| GET    | `/outgoing` | Get invites sent by your team(s) | Student     |
| POST   | `/respond`  | Accept/Reject an invite          | Student     |

---

### WINNER ROUTES (`/api/winners`)

| Method | Route                   | Description              | Access         |
| ------ | ----------------------- | ------------------------ | -------------- |
| GET    | `/`                   | List all winners         | Public         |
| POST   | `/`                   | Add winners for an event | Admin/Convenor |
| PUT    | `/:event_id/:team_id` | Update place             | Admin          |
| DELETE | `/:event_id/:team_id` | Remove winner            | Admin          |

---

### EXEMPTION ROUTES (`/api/exemptions`)

| Method | Route | Description                    | Access |
| ------ | ----- | ------------------------------ | ------ |
| GET    | `/` | List all exemptions            | Admin  |
| POST   | `/` | Exempt a student from an event | Admin  |
| DELETE | `/` | Remove exemption               | Admin  |
