# express

A multi-tenant project and task tracker built with Express 5 and TypeScript. It uses Better Auth with the organization plugin for authentication and role-based access control.

## Status

Early development. The folder structure and tooling are in place. Database, authentication, and feature code are still to be implemented.

## Planned Features

- Email and password authentication
- Organizations with member invitations and active organization switching
- Role-based access control (owner, admin, manager, member, viewer)
- Projects and tasks scoped to the active organization
- Image upload and removal
- Server-rendered pages styled with Tailwind CSS

## Tech Stack

- Express 5
- TypeScript
- Better Auth (organization plugin)
- EJS
- Tailwind CSS v4
- Multer and Sharp for image uploads
- Zod for validation
- Helmet, CORS, and Morgan

## Project Structure

```
express/
├── src/
│   ├── server.ts           # entry point
│   ├── app.ts              # express app and middleware
│   ├── config/             # environment validation
│   ├── lib/                # auth, permissions, db, helpers
│   ├── routes/             # route definitions
│   ├── controllers/        # request handlers
│   ├── services/           # data access and business logic
│   ├── models/             # entity types
│   ├── validations/        # zod schemas
│   ├── middleware/         # auth, organization, permission, upload, errors
│   ├── types/              # shared and Express type extensions
│   ├── styles/             # Tailwind input file
│   └── views/              # EJS layouts, partials, components, pages
├── public/                 # static assets and compiled CSS
├── uploads/                # uploaded images (contents are gitignored)
└── package.json
```

## Getting Started

### Prerequisites

- Node.js 20 or later
- npm

### Installation

```bash
git clone <repository-url>
cd express
npm install
```

### Environment Variables

Copy the example file and fill in the values:

```bash
cp .env.example .env
```

| Variable | Description | Default |
|---|---|---|
| PORT | Port the server listens on | 3000 |
| NODE_ENV | development, production, or test | development |
| BETTER_AUTH_SECRET | Secret used by Better Auth | none |
| BETTER_AUTH_URL | Base URL of the app | http://localhost:3000 |
| MAX_IMAGE_SIZE_MB | Maximum upload size in megabytes | 5 |

### Running in Development

Run the server and the Tailwind watcher in two terminals:

```bash
npm run dev
npm run css:dev
```

The app is available at http://localhost:3000.

### Production Build

```bash
npm run css:build
npm run build
npm start
```

## Scripts

| Script | Description |
|---|---|
| dev | Start the server with file watching (tsx) |
| build | Compile TypeScript to dist |
| start | Run the compiled server |
| css:dev | Build Tailwind CSS and watch for changes |
| css:build | Build and minify Tailwind CSS |

## Roles

| Role | Organization and members | Projects | Tasks |
|---|---|---|---|
| owner | Full, including delete organization | Full | Full |
| admin | Invite and remove members | Full | Full |
| manager | View members | Create, update | Full |
| member | None | Read | Create, update own |
| viewer | None | Read | Read |

These roles are planned and will be defined in `src/lib/permissions.ts`.

