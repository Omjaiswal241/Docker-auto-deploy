# Todo App with Docker Auto-Deploy

A full-stack todo application monorepo with automated Docker Hub deployment using GitHub Actions.

## 🏗️ Project Structure

This monorepo contains the following applications and packages:

### Applications

- **`backend`**: Express.js REST API server (port 8080)
- **`web`**: Next.js frontend application (port 3000)
- **`ws`**: WebSocket server for real-time features (port 8081)

### Packages

- **`db`**: Prisma database client with PostgreSQL adapter and migrations
- **`ui`**: Shared React component library
- **`eslint-config`**: Shared ESLint configurations
- **`typescript-config`**: Shared TypeScript configurations

Each package/app is 100% [TypeScript](https://www.typescriptlang.org/) and uses [Bun](https://bun.sh/) as the runtime.

## 🚀 Quick Start

### Prerequisites

- [Bun](https://bun.sh/) installed
- [Docker](https://www.docker.com/) and Docker Compose installed
- PostgreSQL database (via Docker or local installation)

### Setup

1. **Clone the repository**
   ```bash
   git clone https://github.com/Omjaiswal241/Docker-auto-deploy.git
   cd Docker-auto-deploy
   ```

2. **Install dependencies**
   ```bash
   cd todo-app
   bun install
   ```

3. **Start PostgreSQL database**
   ```bash
   docker run -e POSTGRES_PASSWORD=mysecretpassword -d -p 5432:5432 postgres
   ```

4. **Run database migrations**
   ```bash
   cd packages/db
   bunx prisma migrate deploy
   ```

5. **Start development servers**
   ```bash
   # Backend (from todo-app directory)
   cd apps/backend
   bun run index.ts

   # Frontend (in another terminal)
   cd apps/web
   bun run dev

   # WebSocket (in another terminal)
   cd apps/ws
   bun run index.ts
   ```

## 🐳 Docker Deployment

### Using Docker Compose

Run all services with Docker Compose:

```bash
cd todo-app
docker-compose up
```

This will start:
- Backend API at `http://localhost:8080`
- Frontend at `http://localhost:3000`
- WebSocket server at `http://localhost:8081`
- PostgreSQL database at `localhost:5432`

### Building Individual Images

```bash
# Backend
docker build -t todo-app-backend -f ./docker/Dockerfile.backend .

# Frontend
docker build -t todo-app-frontend -f ./docker/Dockerfile.frontend .

# WebSocket
docker build -t todo-app-ws -f ./docker/Dockerfile.ws .
```

## 🔄 CI/CD Pipeline

This project uses GitHub Actions to automatically build and push Docker images to Docker Hub on every push to the main branch.

### Workflows

- **Backend**: Builds and pushes `omjaiswal241/todo-app-backend`
- **Frontend**: Builds and pushes `omjaiswal241/todo-app-frontend`
- **WebSocket**: Builds and pushes `omjaiswal241/todo-app-ws`

Each image is tagged with:
- `latest` - the most recent build
- `<commit-sha>` - specific commit version

### Setup Secrets

To enable CI/CD, add these secrets to your GitHub repository:
1. Go to Settings → Secrets and variables → Actions
2. Add:
   - `DOCKERHUB_USERNAME`: Your Docker Hub username
   - `DOCKERHUB_PASSWORD`: Your Docker Hub password or access token

## 📦 Database

This project uses Prisma with PostgreSQL.

### Environment Variables

Create `.env` files in:
- `todo-app/packages/db/.env`
- `todo-app/apps/backend/.env`

```env
DATABASE_URL="postgresql://postgres:mysecretpassword@localhost:5432/postgres"
```

### Running Migrations

```bash
cd todo-app/packages/db
bunx prisma migrate dev
```

### Viewing Database

```bash
bunx prisma studio
```

## 🛠️ Development Commands

```bash
# Install dependencies
bun install

# Generate Prisma client
bun run db:generate

# Start backend
bun run start:backend

# Start frontend
bun run start:web

# Start WebSocket server
bun run start:ws
```

## 🧰 Tech Stack

- **Runtime**: Bun
- **Frontend**: Next.js, React
- **Backend**: Express.js
- **WebSocket**: Native WebSocket with Bun
- **Database**: PostgreSQL with Prisma ORM
- **Containerization**: Docker & Docker Compose
- **CI/CD**: GitHub Actions
- **Monorepo**: Turborepo

## 📝 API Endpoints

### Backend (Port 8080)

- `GET /users` - Get all users
- `POST /user` - Create a new user
  - Body: `{ "username": "string", "password": "string" }`

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Commit your changes
4. Push to the branch
5. Open a Pull Request

## 📄 License

MIT
cd my-turborepo

# With [global `turbo`](https://turborepo.dev/docs/getting-started/installation#global-installation) installed (recommended)
turbo login

# Without [global `turbo`](https://turborepo.dev/docs/getting-started/installation#global-installation), use your package manager
npx turbo login
yarn exec turbo login
pnpm exec turbo login
```

This will authenticate the Turborepo CLI with your [Vercel account](https://vercel.com/docs/concepts/personal-accounts/overview).

Next, you can link your Turborepo to your Remote Cache by running the following command from the root of your Turborepo:

```
# With [global `turbo`](https://turborepo.dev/docs/getting-started/installation#global-installation) installed (recommended)
turbo link

# Without [global `turbo`](https://turborepo.dev/docs/getting-started/installation#global-installation), use your package manager
npx turbo link
yarn exec turbo link
pnpm exec turbo link
```

## Useful Links

Learn more about the power of Turborepo:

- [Tasks](https://turborepo.dev/docs/crafting-your-repository/running-tasks)
- [Caching](https://turborepo.dev/docs/crafting-your-repository/caching)
- [Remote Caching](https://turborepo.dev/docs/core-concepts/remote-caching)
- [Filtering](https://turborepo.dev/docs/crafting-your-repository/running-tasks#using-filters)
- [Configuration Options](https://turborepo.dev/docs/reference/configuration)
- [CLI Usage](https://turborepo.dev/docs/reference/command-line-reference)
