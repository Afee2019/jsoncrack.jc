# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

JSON Crack is an open-source JSON visualization and manipulation tool built with Next.js. It transforms JSON, YAML, CSV, XML, and TOML into interactive visual graphs, making data exploration and format conversion easier.

## Key Commands

### Development
```bash
pnpm install          # Install dependencies
pnpm dev             # Start dev server on port 3078
pnpm build           # Build for production (static export)
pnpm start           # Serve static build on port 3078
pnpm start:next      # Start Next.js production server
```

### Code Quality
```bash
pnpm lint            # Run TypeScript check, ESLint, and Prettier check
pnpm lint:fix        # Auto-fix ESLint and Prettier issues
pnpm analyze         # Analyze bundle size
```

### Docker
```bash
docker compose build  # Build Docker image
docker compose up     # Run locally on port 8888
```

## Architecture

### Tech Stack
- **Framework**: Next.js 15 with static export (`output: "export"`)
- **UI Library**: Mantine v7
- **State Management**: Zustand
- **Styling**: Styled Components
- **Graph Visualization**: Reaflow (React Flow wrapper)
- **Code Editor**: Monaco Editor
- **Data Processing**: Various parsers (jsonc-parser, js-yaml, fast-xml-parser)

### Core Directory Structure
- `src/pages/` - Next.js pages (editor, converters, type generators)
- `src/features/` - Feature-specific components
  - `editor/` - Main editor interface components
  - `modals/` - Various modal dialogs
- `src/store/` - Zustand stores for global state
- `src/lib/utils/` - Utility functions and helpers
- `src/constants/` - Constants and configurations

### Key Stores (Zustand)
- `useFile` - Manages file content and format
- `useJson` - Handles JSON parsing and validation
- `useConfig` - Editor configuration settings
- `useModal` - Modal state management
- `useGraph` - Graph visualization state

### Data Flow
1. User inputs data via Monaco Editor or file upload
2. Data is parsed based on format (JSON/YAML/CSV/XML/TOML)
3. Parser generates graph nodes and edges
4. Reaflow renders the interactive graph visualization
5. User can export, convert, or manipulate the data

## Code Standards

### TypeScript & Linting
- TypeScript with `strict: true` (except `noImplicitAny: false`)
- ESLint with Next.js and TypeScript rules
- Prettier for formatting with 100-char line width
- Double quotes for strings
- Unix line endings
- Semicolons required

### Import Order (enforced by Prettier)
1. React imports
2. Next.js imports
3. Mantine core
4. Other Mantine
5. Styled components
6. Third-party modules
7. Internal src/ imports
8. Relative imports

### Key Patterns
- Dynamic imports for modals and heavy components
- WebAssembly for performance-critical operations (json_typegen_wasm)
- Local-only data processing (privacy-focused)
- Debounced content updates to prevent excessive re-renders

## Environment Variables
- `NEXT_PUBLIC_NODE_LIMIT` - Maximum nodes in graph visualization (default: 800)
- `NEXT_TELEMETRY_DISABLED` - Disable Next.js telemetry

## Important Considerations
- All data processing is client-side for privacy
- Static export means no server-side features
- Graph performance degrades with >800 nodes
- Uses WebAssembly for type generation
- Sentry integration only in production builds