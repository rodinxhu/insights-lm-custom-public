# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

InsightsLM is an open-source, self-hostable alternative to NotebookLM built with React/TypeScript frontend and Supabase backend. The application allows users to upload documents, chat with their content using RAG (Retrieval-Augmented Generation), and generate audio overviews.

## Development Commands

### Building and Development
- `npm run dev` - Start development server with Vite
- `npm run build` - Build for production
- `npm run build:dev` - Build for development mode
- `npm run preview` - Preview production build
- `npm run lint` - Run ESLint

### Testing
Currently no test commands are defined in package.json. Tests would need to be added.

## Architecture Overview

### Frontend Stack
- **React 18** with TypeScript
- **Vite** as build tool and dev server
- **shadcn/ui** component library built on Radix UI
- **Tailwind CSS** for styling
- **React Router** for routing
- **TanStack Query** for API state management
- **Supabase JS** client for backend integration

### Backend Architecture
- **Supabase** - PostgreSQL database, authentication, storage, and Edge Functions
- **N8N workflows** - Handle complex backend automation and AI processing
- **Vector embeddings** - pgvector extension for semantic search

### Database Schema
Core entities:
- `profiles` - User profiles linked to auth
- `notebooks` - Main containers for sources and notes
- `sources` - Documents/URLs uploaded to notebooks (pdf, text, website, youtube, audio)
- `notes` - Generated or user-created content within notebooks
- `documents` - Vector embeddings for RAG functionality
- `n8n_chat_histories` - Chat session storage

### Key Directories

```
src/
├── components/          # React components
│   ├── auth/           # Authentication components
│   ├── chat/           # Chat interface components
│   ├── dashboard/      # Main dashboard components
│   ├── notebook/       # Notebook-specific components
│   └── ui/             # shadcn/ui component library
├── contexts/           # React contexts (AuthContext)
├── hooks/              # Custom React hooks
├── integrations/       # External service integrations
│   └── supabase/       # Supabase client and types
├── pages/              # Page components
├── services/           # Service layer functions
└── types/              # TypeScript type definitions

supabase/
├── functions/          # Edge Functions (serverless functions)
└── migrations/         # Database migrations

n8n/                    # N8N workflow definitions (JSON files)
```

### State Management Pattern
- **Authentication**: Context API with `AuthContext`
- **API Data**: TanStack Query for server state
- **Component State**: React hooks (useState, useEffect)
- **Custom Hooks**: Encapsulate complex state logic (e.g., `useNotebooks`, `useSources`)

### Route Structure
- `/` - Dashboard (protected)
- `/notebook/:id` - Individual notebook view (protected)
- `/auth` - Authentication page

### Component Architecture
- **Pages** act as route handlers and compose layouts
- **Components** are organized by feature domain
- **UI Components** use shadcn/ui pattern with Radix UI primitives
- **Hooks** handle data fetching and complex state logic

### Supabase Integration
- Edge Functions handle complex workflows via N8N webhooks
- Row Level Security (RLS) enforces data access permissions
- Real-time subscriptions used for live updates
- File storage for document uploads

### N8N Workflow Integration
The application uses N8N workflows for:
- Document processing and content extraction
- AI-powered notebook content generation
- Audio overview generation
- Chat message processing with RAG

Key webhook URLs stored in Supabase secrets:
- `NOTEBOOK_CHAT_URL`
- `NOTEBOOK_GENERATION_URL`
- `AUDIO_GENERATION_WEBHOOK_URL`
- `DOCUMENT_PROCESSING_WEBHOOK_URL`
- `ADDITIONAL_SOURCES_WEBHOOK_URL`

### Environment Variables
Required in `.env.local`:
- `VITE_SUPABASE_URL` - Supabase project URL
- `VITE_SUPABASE_ANON_KEY` - Supabase anonymous key

### Key Development Patterns
- Components use TypeScript with proper type definitions from `src/integrations/supabase/types.ts`
- Error boundaries and loading states handled consistently
- Mobile-responsive design with conditional rendering based on screen size
- Optimistic updates with TanStack Query mutations
- File uploads handled through Supabase storage with progress tracking

### Important Implementation Details
- The app uses Loveable's component tagger in development mode
- Vector similarity search implemented via `match_documents` database function
- Audio URLs have expiration handling with refresh mechanisms
- Real-time collaboration features through Supabase subscriptions
- Source processing status tracked through database enums

## AI/LLM Integration Points
- Chat functionality uses RAG with vector embeddings
- OpenAI integration for title generation and chat responses
- Audio generation capabilities for podcast-style overviews
- Document content extraction and summarization

When working with this codebase, pay attention to the N8N workflow dependencies and ensure Supabase Edge Functions are properly configured for the full application functionality.