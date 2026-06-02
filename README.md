# QMOS (Community Operating System)

Production-grade PERN (PostgreSQL, Express, React, Node) foundation setup for the QMOS Community Operating System.

## Project Structure

This project uses an industry-standard directory structure to separate the frontend client and backend server environments:

```
QMOS/
├── .gitignore                 # Root git ignore rules
├── .nvmrc                     # Node Version Manager config (Node LTS v20.12.2)
├── .node-version              # Node.js version reference
├── README.md                  # Root documentation and commands
├── client/                    # React + Vite + TypeScript frontend application
│   └── .env.example           # Client-side environment variables template
└── server/                    # Node.js + Express + TypeScript backend application
    └── .env.example           # Server-side environment variables template
```

---

## Getting Started

### Prerequisites

- **Package Manager**: [pnpm](https://pnpm.io/) (Recommended)
- **Node.js**: LTS v20.x or v22.x (Specified version: `20.12.2`)

To ensure you are using the correct Node.js version, run:
```bash
nvm use
```

---

## Step 2 Initialization Commands (Next Step)

Once the foundation is verified, the next step will run the following initialization sequences:

### 1. Initialize Client (React + Vite + TS)

Run these commands inside the `client` directory:
```bash
# Navigate to client directory
cd client

# Scaffold the React TypeScript Vite project
pnpm create vite . --template react-ts

# Install baseline dev dependencies (No UI/feature packages yet)
pnpm install
```

### 2. Initialize Server (Node.js + Express + TS)

Run these commands inside the `server` directory:
```bash
# Navigate to server directory
cd server

# Initialize Node project package manifest
pnpm init

# Install backend core libraries
pnpm add express cors dotenv helmet morgan pg

# Install development toolchain and typings
pnpm add -D typescript @types/node @types/express @types/cors @types/morgan tsx nodemon
```

---

## Development Naming Conventions

To ensure high-quality, production-ready code consistency, please adhere to:

| Category | Convention | Examples |
| :--- | :--- | :--- |
| **Files & Directories** | `kebab-case` | `user-profile.tsx`, `db-connection.ts` |
| **React Components** | `PascalCase` | `UserProfile.tsx`, `Button.tsx` |
| **Variables & Functions** | `camelCase` | `getUserData`, `apiBaseUrl` |
| **Types & Interfaces** | `PascalCase` | `UserPayload`, `DatabaseConfig` |
| **CSS Class Names** | `kebab-case` | `btn-primary`, `nav-item` |
