# Generic Backend Example

Template for managing a backend-only service (API, microservice, CLI tool, etc.).

## Project Setup

- **Framework**: Django, FastAPI, Express, Go, etc.
- **Database**: PostgreSQL, MongoDB, etc.
- **API**: RESTful or GraphQL
- **Tests**: pytest, unittest, mocha, etc.
- **Deployment**: Docker, Kubernetes, serverless, etc.

## Project Structure

```
backend-service/
├── app/              # Application code
│   ├── models.py     # Database models
│   ├── views.py      # API endpoints (Django) or routers (FastAPI)
│   ├── serializers.py # Data serialization
│   ├── tests/        # Unit and integration tests
│   └── utils.py      # Helper functions
├── tests/            # Test suite
├── migrations/       # Database migrations
├── requirements.txt  # Dependencies
├── .env              # Environment variables
├── manage.py         # Django management
└── .claude/          # Claude Code config
```

## Commands

```bash
/backend-dev       # Start development server
/backend-test      # Run test suite
/backend-migrate   # Run database migrations
/backend-lint      # Check code quality
/backend-debug     # Debug specific endpoint
/backend-deploy    # Deploy to environment
```

## Key Workflows

### Development Workflow

```bash
1. Create feature branch
2. Write failing test
3. Implement minimal code to pass test
4. Run full test suite
5. Commit changes
6. Push to remote
7. Create pull request
```

### Database Migration

```bash
# Make changes to models.py
python manage.py makemigrations

# Review migration file
cat app/migrations/XXXX_auto.py

# Apply migration
python manage.py migrate

# Commit
git commit -m "migration: add new field to User model"
```

### Testing

```bash
# Run all tests
pytest

# Run specific test file
pytest tests/test_api.py

# Run with coverage
pytest --cov=app

# Watch for changes
pytest-watch
```

### Deployment

```bash
# 1. Run tests
pytest --cov

# 2. Build application
docker build -t service:latest .

# 3. Push to registry
docker push registry/service:latest

# 4. Deploy to environment
kubectl apply -f deployment.yaml

# 5. Verify deployment
curl https://api.example.com/health
```

## Common Patterns

### API Endpoint Structure

```python
# models.py — Database schema
class User(models.Model):
    name = models.CharField(max_length=100)
    email = models.EmailField()
    created_at = models.DateTimeField(auto_now_add=True)

# serializers.py — Data format
class UserSerializer(serializers.ModelSerializer):
    class Meta:
        model = User
        fields = ['id', 'name', 'email', 'created_at']

# views.py — API logic
@api_view(['GET', 'POST'])
def user_list(request):
    if request.method == 'GET':
        users = User.objects.all()
        serializer = UserSerializer(users, many=True)
        return Response(serializer.data)
    elif request.method == 'POST':
        serializer = UserSerializer(data=request.data)
        if serializer.is_valid():
            serializer.save()
            return Response(serializer.data, status=201)
        return Response(serializer.errors, status=400)

# tests/test_api.py — Testing
def test_get_users():
    User.objects.create(name='John', email='john@example.com')
    response = client.get('/api/users/')
    assert response.status_code == 200
    assert len(response.data) == 1
```

### Error Handling

```python
# Handle common errors
try:
    user = User.objects.get(id=user_id)
except User.DoesNotExist:
    return Response({'error': 'User not found'}, status=404)
except Exception as e:
    logger.error(f'Error fetching user: {e}')
    return Response({'error': 'Internal error'}, status=500)
```

### Async Tasks

```python
# tasks.py — Celery tasks
@shared_task
def send_welcome_email(user_id):
    user = User.objects.get(id=user_id)
    # Send email asynchronously

# views.py — Trigger task
@api_view(['POST'])
def create_user(request):
    serializer = UserSerializer(data=request.data)
    if serializer.is_valid():
        user = serializer.save()
        send_welcome_email.delay(user.id)  # Async task
        return Response(serializer.data, status=201)
    return Response(serializer.errors, status=400)
```

## Environment Setup

```bash
# Create virtual environment
python -m venv venv
source venv/bin/activate

# Install dependencies
pip install -r requirements.txt

# Create .env file
cp .env.example .env
# Edit .env with your settings

# Run migrations
python manage.py migrate

# Start server
python manage.py runserver
```

## Performance Optimization

- **N+1 Query Problem** — Use `select_related()` and `prefetch_related()`
- **Caching** — Redis for frequently accessed data
- **Indexing** — Add database indexes for common queries
- **Pagination** — Limit results, implement cursor-based pagination
- **Async Processing** — Long-running tasks → Celery

## Monitoring & Logging

```python
import logging

logger = logging.getLogger(__name__)

# Log important events
logger.info(f'User created: {user.id}')
logger.error(f'Failed to process payment: {error}')

# Monitor with external service (Sentry, DataDog, etc.)
capture_exception(e)
```

## Next Steps

1. Customize CLAUDE.md for your backend
2. Set up development environment
3. Configure testing pipeline
4. Set up deployment automation
5. Document API endpoints

---

Use this template when managing backend services.
