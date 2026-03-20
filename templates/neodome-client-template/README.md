# Neodome Client Template

A production-ready Vite + Firebase starter kit for rapid SaaS deployment.

## Why This Template?

This is the foundation I use to spin up production infrastructure in minutes. Every client project starts here — a fully configured, production-ready template that proves what I build from day one.

## Project Structure

```
neodome-client-template/
├── src/
│   ├── components/           # React components
│   │   ├── layout/           # Layout components (Header, Footer, Sidebar)
│   │   └── ui/               # Reusable UI primitives
│   ├── hooks/                # Custom React hooks
│   ├── lib/                  # Utilities and helpers
│   │   └── firebase.ts       # Firebase configuration
│   ├── pages/                # Route components
│   │   └── Home.tsx
│   ├── stores/               # State management
│   ├── styles/               # Global styles and theme
│   ├── types/                # TypeScript type definitions
│   ├── App.tsx               # Root component
│   └── main.tsx              # Entry point
├── public/                   # Static assets
├── functions/                # Firebase Cloud Functions
│   ├── src/
│   │   ├── index.ts          # Function exports
│   │   ├── auth/             # Auth-related functions
│   │   ├── api/              # API route handlers
│   │   └── utils/            # Function utilities
│   ├── package.json
│   └── tsconfig.json
├── tests/                    # Test suite
│   ├── unit/
│   ├── integration/
│   └── e2e/
├── .env.example              # Environment variable template
├── .gitignore
├── firebase.json             # Firebase configuration
├── firestore.rules           # Firestore security rules
├── firestore.indexes.json    # Firestore indexes
├── package.json
├── tsconfig.json
├── vite.config.ts
└── README.md
```

## What's Pre-Configured

- **Vite 5** — Lightning-fast builds and HMR
- **TypeScript** — Full type safety
- **Firebase Auth** — Authentication with Google, email/password
- **Firestore** — Real-time database with security rules
- **Cloud Functions** — Serverless backend logic
- **Testing** — Unit, integration, and E2E test setup
- **CI/CD** — GitHub Actions workflows for deploys

## Getting Started

```bash
# Clone the template
git clone https://github.com/neodome/neodome-client-template my-project
cd my-project

# Install dependencies
npm install

# Copy environment variables
cp .env.example .env.local

# Start development server
npm run dev
```

## Next Steps

1. Configure Firebase project in `.env.local`
2. Set up Firestore security rules for your data model
3. Deploy Cloud Functions for your API needs
4. Customize the theme in `src/styles/`

---

Built with [NeoDome](https://neodigium.com)
