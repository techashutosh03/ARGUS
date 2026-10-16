# Friday AI System

## Architecture Overview

```text
friday-ai-system/                  # Root
├── apps/
│   ├── web/                       # Next.js 15 Dashboard + APIs (Ashutosh leads)
│   │   ├── app/
│   │   │   ├── (auth)/            # Clerk auth routes
│   │   │   ├── (dashboard)/       # Main control panel, memory viewer, settings
│   │   │   ├── api/               # tRPC + Route Handlers (your main backend)
│   │   │   └── layout.tsx
│   │   ├── components/            # Reusable UI (using shadcn/ui)
│   │   ├── lib/
│   │   │   ├── supabase.ts        # Supabase client + RLS helpers
│   │   │   ├── clerk.ts
│   │   │   ├── encryption.ts      # Web Crypto + envelope encryption
│   │   │   └── two-phase-storage.ts
│   │   ├── hooks/
│   │   ├── types/
│   │   ├── trpc/                  # tRPC router (your REST-like APIs)
│   │   ├── utils/
│   │   └── next.config.mjs
│   │
│   └── extension/                 # Plasmo Browser Extension (Dev leads)
│       ├── src/
│       │   ├── background/        # Background scripts, messaging to backend
│       │   ├── content/           # DOM scraping, cleaning, adaptive selectors
│       │   ├── popup/             # Human-in-the-Loop dynamic popups
│       │   ├── sidepanel/         # Main Friday UI panel
│       │   ├── options/           # Settings page
│       │   ├── components/
│       │   ├── lib/
│       │   │   ├── messaging.ts   # Communication with web backend
│       │   │   ├── scraper.ts
│       │   │   └── realtime.ts    # Supabase Realtime listener
│       │   └── manifest.config.ts
│       ├── package.json
│       └── plasmo.config.ts
│
├── packages/
│   ├── ui/                        # Shared shadcn/ui components (both use)
│   ├── types/                     # Shared TypeScript types (critical)
│   │   └── index.ts               # User, Memory, AgentState, etc.
│   ├── db/                        # Drizzle + Supabase schema (Ashutosh owns)
│   │   ├── schema.ts              # All tables (users, memories, tokens, audit_logs, etc.)
│   │   ├── client.ts
│   │   └── rls-policies.sql
│   ├── agents/                    # LangGraph workflows (Dev owns)
│   │   ├── friday-agent.ts        # Main agent graph
│   │   ├── tools/                 # Browser tools, memory tools, human-in-loop
│   │   ├── memory.ts              # Two-phase memory implementation
│   │   └── checkpoints.ts         # Human-in-the-loop logic
│   ├── encryption/                # Shared encryption utilities (Ashutosh owns)
│   ├── llm/                       # LiteLLM router + prompt templates
│   ├── scraping/                  # Shared scraping helpers & LLM-based cleaners
│   └── utils/                     # Common utilities (date, validation, logging)
│
├── turbo.json
├── package.json
├── tsconfig.json
├── .env.example
├── .gitignore
├── README.md                      # Full architecture explanation + setup guide
└── docs/
    ├── security-model.md
    ├── two-phase-memory.md
    └── agent-workflows.md
```

## System Components

### Applications
- **apps/web**: Next.js 15 dashboard, tRPC backend routes, Clerk authentication, and user control panels.
- **apps/extension**: Plasmo browser extension providing the sidepanel UI, background tasks, DOM scraping, and human-in-the-loop workflows.

### Shared Packages
- **packages/ui**: Reusable design system and UI components based on shadcn/ui.
- **packages/types**: Core shared TypeScript types (User, Memory, AgentState, etc.).
- **packages/db**: Database layer with Drizzle ORM, Supabase client, and Row Level Security (RLS) policies.
- **packages/agents**: LangGraph agent workflows, tools, checkpoints, and two-phase memory logic.
- **packages/encryption**: Envelope encryption and Web Crypto utilities.
- **packages/llm**: LiteLLM router and prompt templates.
- **packages/scraping**: Scraping helpers and LLM-based DOM cleaners.
- **packages/utils**: General utility functions.

### Documentation
- `docs/security-model.md`: Security architecture, encryption model, and RLS guidelines.
- `docs/two-phase-memory.md`: Design and lifecycle of the two-phase memory system.
- `docs/agent-workflows.md`: LangGraph execution graphs and human-in-the-loop interaction patterns.
