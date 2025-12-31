# ChronoSync: Visualizing Causality in Distributed Systems

![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)
![Go 1.21+](https://img.shields.io/badge/go-1.21+-00ADD8.svg)
![Next.js 14](https://img.shields.io/badge/Next.js-14-black)
![TypeScript 5](https://img.shields.io/badge/TypeScript-5-blue)

ChronoSync is an open-source tool that visualizes causality in distributed systems by transforming vector clock logs into interactive diagrams. It makes the invisible happens-before relationship tangible for engineers, helping detect complex bugs that traditional AI tools often miss.

## 🎯 Why ChronoSync?
Modern distributed systems are notoriously difficult to debug. Traditional logs and tracing tools show you what happened, but ChronoSync shows you why it happened by visualizing the causal relationships between events across different nodes.

## Key Features
- **Interactive Causality Visualization**: Transform vector clock traces into intuitive graphs and timelines
- **Anomaly Detection**: Identify causality violations, race conditions, and ordering inconsistencies
- **WASM-Powered Engine**: Perform complex causal analysis directly in the browser
- **Multiple Input Formats**: Support for various log formats (JSON, custom structured logs)
- **CLI Tool**: Analyze traces locally from your terminal
- **Developer SDK**: Instrument your Go applications to generate compatible traces

## 🏗️ Project Architecture
ChronoSync follows a modern monorepo architecture with clear separation of concerns:

```

chrono-sync/
├── .github/
│   ├── workflows/
│   │   ├── test-go.yml
│   │   ├── build-wasm.yml
│   │   └── deploy-nextjs.yml
│   └── ISSUE_TEMPLATE/
│
├── apps/                          # ALL APPLICATIONS LIVE HERE
│   ├── chrono-sync-web/                    # NEXT.JS FRONTEND APP
│   │   ├── public/
│   │   │   ├── wasm/              # Compiled WASM from Go
│   │   │   │   └── engine.wasm
│   │   │   ├── favicon.ico
│   │   │   └── robots.txt
│   │   ├── src/
│   │   │   ├── app/               # App Router (Next.js 13+)
│   │   │   │   ├── layout.tsx
│   │   │   │   ├── page.tsx       # Main visualization page
│   │   │   │   ├── api/           # API routes (if needed)
│   │   │   │   │   └── analyze/
│   │   │   │   │       └── route.ts
│   │   │   │   └── about/
│   │   │   │       └── page.tsx
│   │   │   ├── components/        # React components
│   │   │   │   ├── ui/           # Base UI (shadcn/ui)
│   │   │   │   ├── visualization/
│   │   │   │   │   ├── VectorGraph.tsx  # D3/Cytoscape visualization
│   │   │   │   │   ├── Timeline.tsx
│   │   │   │   │   └── AnomalyList.tsx
│   │   │   │   ├── upload/
│   │   │   │   │   └── FileUpload.tsx
│   │   │   │   └── layout/
│   │   │   │       ├── Header.tsx
│   │   │   │       └── Sidebar.tsx
│   │   │   ├── lib/              # Frontend utilities
│   │   │   │   ├── wasm/
│   │   │   │   │   ├── loader.ts # WASM initialization
│   │   │   │   │   └── types.ts  # TypeScript definitions
│   │   │   │   ├── graph/
│   │   │   │   │   ├── layout.ts # Graph layout algorithms
│   │   │   │   │   └── render.ts # D3 rendering logic
│   │   │   │   └── utils/
│   │   │   │       └── parsers.ts
│   │   │   ├── types/            # TypeScript types
│   │   │   │   ├── vctrace.ts    # Log format types
│   │   │   │   └── graph.ts      # Graph data types
│   │   │   ├── styles/
│   │   │   │   └── globals.css
│   │   │   └── hooks/            # Custom React hooks
│   │   │       └── useWasm.ts
│   │   ├── package.json          # Next.js dependencies
│   │   ├── next.config.js        # Next.js configuration
│   │   ├── tailwind.config.js    # Tailwind CSS config
│   │   ├── tsconfig.json         # TypeScript config
│   │   └── README.md
│   │
│   └── cli/                      # CLI TOOL (Go)
│       └── main.go               # CLI entry point
│
├── packages/                     # SHARED PACKAGES & LIBS
│   ├── core/                     # GO CORE ENGINE
│   │   ├── internal/            # Private Go code
│   │   │   ├── parser/
│   │   │   ├── detector/
│   │   │   └── web/
│   │   ├── pkg/                 # Public Go libraries
│   │   │   ├── clock/
│   │   │   ├── graph/
│   │   │   ├── formats/
│   │   │   └── sdk/
│   │   ├── cmd/                 # Go executables
│   │   │   ├── wasm/           # WASM build target
│   │   │   │   └── main.go
│   │   │   └── server/         # Optional Go HTTP server
│   │   │       └── main.go
│   │   ├── go.mod              # Go module for core
│   │   └── go.sum
│   │
│   ├── shared-types/            # SHARED TYPESCRIPT TYPES
│   │   ├── src/
│   │   │   ├── index.ts
│   │   │   ├── vctrace.ts       # Shared log format types
│   │   │   └── graph.ts         # Shared graph types
│   │   ├── package.json
│   │   └── tsconfig.json
│   │
│   └── sdk-go/                  # GO INSTRUMENTATION SDK
│       ├── go.mod
│       └── sdk.go
│
├── examples/                    # DEMO & EXAMPLE TRACES
│   ├── basic-trace/
│   │   ├── trace.json
│   │   ├── generate.go
│   │   └── README.md
│   ├── demo-anomaly/
│   └── integration/
│
├── tests/                       # TEST SUITES
│   ├── testdata/
│   ├── unit/
│   ├── integration/
│   └── e2e/                     # End-to-end tests
│       ├── playwright.config.ts
│       └── app.spec.ts
│
├── scripts/
│   ├── build-all.sh
│   ├── build-wasm.sh
│   └── setup-dev.sh
│
├── docs/
│   ├── ARCHITECTURE.md
│   ├── API.md
│   └── CONTRIBUTING.md
│
├── docker-compose.yml           # Local development
├── package.json                 # Root package.json (workspaces)
├── turbo.json                   # Turborepo configuration
├── .gitignore
├── .eslintrc.json
├── .prettierrc
├── LICENSE
└── README.md

```

## 🚀 Quick Start
### Prerequisites
- Node.js 18+ and npm/yarn/pnpm
- Go 1.21+
- Git



---
**ChronoSync**: Making distributed system causality visible, one trace at a time.

