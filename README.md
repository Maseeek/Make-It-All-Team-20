# Make-It-All

An internal staff app that combines a discussion forum with project task tracking, built as a university team project for a fictional company called Make-It-All.

## What it does

- Staff sign in with a company email. Only pre-approved employees can register, and each email can hold one account.
- Users have roles (admin, manager, project manager, technical specialist), and each role sees and can do different things.
- A forum with topics and posts. Technical specialists, managers and admins can post; only admins can delete.
- Project tasks: project managers create and assign tasks, and assignees update the status and time spent.
- Managers can see every user and the tasks assigned to them.
- A personal to-do board with To-Do, Working and Done columns and drag-and-drop between them.

## How it's built

- Frontend: React 18, Vite and React Router, with a fetch-based service layer per feature (`client/src/services`).
- Backend: Node.js and Express with a SQLite database. The schema (users, topics, posts, project tasks, to-dos) is created from a script on startup. The team planned to move to MySQL on the university servers, and an early MySQL setup is in `server/db/_mysql`.
- Auth: passwords are hashed with bcrypt and sessions use JWTs. Two small Express middlewares, `isAuthorized` and `hasRoles(...)`, guard every forum and task route, so access rules sit next to the routes they protect.
- Registration checks the email domain, an allowlist of staff and existing accounts before creating a user. The register form also checks password strength (8+ characters with upper and lower case, a number and a symbol).

## My role

I wrote the login and register flow (React forms, password checks and the register endpoint), the navbar, and the app's colour scheme and dark styling. I also set up role access across the dashboard, to-dos and tasks, and seeded the test accounts used during development.

## Run it locally

You need Node.js 16 or newer.

```bash
git clone https://github.com/Maseeek/Make-It-All-Team-20.git
cd Make-It-All-Team-20
npm run install:all
cp .env.example .env
npm run dev
```

The frontend runs at http://localhost:5173 and the API at http://localhost:3000 (health check at `/api/health`). The server seeds a few test accounts on startup; see `server/index.js`.

## Status

This is a coursework prototype. The personal to-do board keeps its items in the browser only, and the manager analytics endpoints in `server/routes/dashboard.js` are still stubs.

MIT licensed. See [LICENSE](LICENSE).
