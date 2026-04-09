# Taleemabad CMS Example

Real working example of a React SPA (Single Page Application) for content management.

## Project Setup

- **Framework**: React 19 + Vite
- **Language**: TypeScript
- **Styling**: TailwindCSS
- **Backend**: Django REST API
- **Storage**: AWS S3 (presigned URLs for uploads)

## Key Features

- **Media Asset Management** — Searchable asset library, file uploads to S3
- **Training Management** — Create trainings, link assets, build quizzes
- **S3 Upload** — Browser-to-S3 uploads with progress tracking
- **Admin Dashboard** — Overview, quick actions, status cards

## CLAUDE.md Configuration

See [CLAUDE.md](./CLAUDE.md) for how to integrate this project into your workflow:

- Auto-start tasks specific to CMS
- Project-specific commands (`/cms-dev`, `/cms-test`)
- MCP servers for frontend development
- Error handling for common CMS issues

## Directory Structure

```
repos/taleemabad-cms/
├── src/
│   ├── components/           # React components
│   ├── pages/                # Page components
│   ├── hooks/                # Custom React hooks (including useS3Upload)
│   ├── utils/                # Utility functions
│   └── types/                # TypeScript types
├── public/                    # Static assets
├── .env                       # Environment variables (VITE_API_BASE_URL, etc.)
├── vite.config.ts            # Vite configuration
├── tsconfig.json             # TypeScript configuration
└── .claude/                  # Claude Code config
    ├── QUICK-REF.md          # Quick reference for CMS patterns
    └── agents.json           # Agent configuration
```

## Commands

```bash
# Development
npm run dev          # Start dev server
npm run build        # Build for production
npm run preview      # Preview production build
npm run type-check   # TypeScript validation

# Testing
npm test             # Run tests
npm run lint         # Run linter

# S3 Integration
# Uses VITE_API_BASE_URL to generate presigned URLs
# Backend endpoint: POST /api/v1/internal/media_assets/presigned_upload_url/
```

## Key Integrations

### S3 Upload Flow

1. **Frontend** — `useS3Upload` hook handles file selection and upload
2. **Backend** — Presigned URL endpoint generates temporary S3 credentials
3. **Browser** — Direct upload to S3 with progress tracking
4. **Asset Form** — File picker → upload → populate S3 URL

### Training Form

- Searchable dropdown for linking assets to trainings
- Auto-save drafts
- Quiz builder integration
- Status tracking

## Common Issues & Solutions

See [CLAUDE.md](./CLAUDE.md) error recovery section for:
- Build failures
- S3 CORS issues
- API connectivity problems
- TypeScript errors

## Next Steps

1. Copy `CLAUDE.md` template (from parent scaffold/)
2. Customize project section for CMS
3. Configure `/cms-dev` and `/cms-test` commands
4. Read quick reference: `.claude/QUICK-REF.md`

---

Use this as a reference when working on your own frontend projects.
