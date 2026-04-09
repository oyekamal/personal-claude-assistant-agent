# Generic SaaS Example

Template for managing a SaaS product with separate backend and frontend teams/projects.

## Project Structure

```
saas-product/
├── backend/           # Django/FastAPI/Node backend
├── frontend/          # React/Vue frontend
├── docs/              # Shared documentation
└── devops/            # Infrastructure and deployment
```

## Backend Setup

- **Framework**: Django (or FastAPI, Express, etc.)
- **Database**: PostgreSQL
- **API**: RESTful or GraphQL
- **Async**: Celery for background jobs
- **Storage**: S3 for file uploads

### Commands

```bash
/saas-be-dev       # Start backend dev server
/saas-be-test      # Run tests
/saas-be-migrate   # Run migrations
/saas-be-deploy    # Deploy to environment
```

## Frontend Setup

- **Framework**: React 19 (or Vue, Svelte, etc.)
- **Build**: Vite or Webpack
- **Styling**: TailwindCSS
- **API**: Fetch or axios
- **Testing**: Vitest or Jest

### Commands

```bash
/saas-fe-dev       # Start frontend dev server
/saas-fe-test      # Run tests
/saas-fe-build     # Build for production
/saas-fe-deploy    # Deploy to CDN
```

## Shared Patterns

### API Integration

Frontend calls backend APIs:

```typescript
// Frontend hooks/useApi.ts
const fetchTrainings = async () => {
  const response = await fetch(`${API_BASE_URL}/api/v1/trainings/`);
  return response.json();
};
```

Backend provides endpoints:

```python
# Backend views.py
@api_view(['GET'])
def training_list(request):
    trainings = Training.objects.all()
    return Response(TrainingSerializer(trainings, many=True).data)
```

### Database Migrations

Backend handles schema changes:

```bash
python manage.py makemigrations
python manage.py migrate
```

Frontend adapts to API schema changes.

### Deployment Pipeline

```
1. Local development (dev servers)
2. Automated tests (CI/CD)
3. Staging environment (integration testing)
4. Production deployment (with monitoring)
```

## Environment Variables

### Backend

```
DATABASE_URL=postgresql://...
SECRET_KEY=...
AWS_S3_BUCKET=...
FRONTEND_URL=...
```

### Frontend

```
VITE_API_BASE_URL=http://localhost:8000
VITE_ENV=development
```

## Next Steps

1. Customize CLAUDE.md for your SaaS
2. Define project-specific commands
3. Set up CI/CD pipeline
4. Configure environment variables
5. Document API contracts

---

Use this template when managing multi-service applications.
