# Tech Stack Reference

Detailed configurations for common technology stacks.

## Frontend Stacks

### React + TypeScript + Vite

**Structure:**
```
src/
├── components/
├── hooks/
├── pages/
├── services/
├── types/
├── utils/
├── App.tsx
├── main.tsx
└── vite.config.ts
```

**Dependencies:**
```json
{
  "devDependencies": {
    "@types/react": "^18",
    "@vitejs/plugin-react": "^4",
    "typescript": "^5",
    "vite": "^5"
  },
  "dependencies": {
    "react": "^18",
    "react-dom": "^18",
    "react-router-dom": "^6"
  }
}
```

**Config Files:**
- vite.config.ts
- tsconfig.json
- .eslintrc.cjs
- postcss.config.js
- tailwind.config.js (if using Tailwind)

**CI Workflow**: Test → Lint → Build → Deploy

### Next.js (App Router)

**Structure:**
```
src/
├── app/
│   ├── page.tsx
│   ├── layout.tsx
│   └── api/
├── components/
├── lib/
├── hooks/
├── types/
└── utils/
```

**Dependencies:**
```json
{
  "dependencies": {
    "next": "14",
    "react": "18",
    "react-dom": "18"
  },
  "devDependencies": {
    "@types/node": "^20",
    "typescript": "^5"
  }
}
```

**Config Files:**
- next.config.js
- tsconfig.json
- tailwind.config.ts (if using Tailwind)
- .eslintrc.json

**Topics**: `nextjs, nextjs14, react, typescript, serverless`

### Vue 3 + Vite

**Structure:**
```
src/
├── components/
├── views/
├── router/
├── stores/
├── composables/
├── assets/
├── App.vue
└── main.ts
```

**Dependencies:**
```json
{
  "dependencies": {
    "vue": "^3",
    "vue-router": "^4",
    "pinia": "^2"
  },
  "devDependencies": {
    "@vitejs/plugin-vue": "^5",
    "typescript": "^5",
    "vite": "^5"
  }
}
```

**Topics**: `vue3, vite, typescript, pinia, vue-router`

## Backend Stacks

### Node.js + Express + TypeScript

**Structure:**
```
src/
├── config/
├── controllers/
├── middleware/
├── models/
├── routes/
├── services/
├── utils/
├── app.ts
└── server.ts
```

**Dependencies:**
```json
{
  "dependencies": {
    "express": "^4",
    "cors": "^2",
    "dotenv": "^16",
    "mongoose": "^8",
    "zod": "^3"
  },
  "devDependencies": {
    "@types/express": "^4",
    "typescript": "^5",
    "ts-node": "^10",
    "nodemon": "^3"
  }
}
```

**Topics**: `express, nodejs, typescript, rest-api, mongodb`

### FastAPI + Python

**Structure:**
```
src/
├── api/
│   └── routes/
├── core/
├── models/
├── schemas/
├── services/
├── utils/
├── main.py
└── config.py
```

**Dependencies:**
```toml
dependencies = [
    "fastapi>=0.100",
    "uvicorn>=0.23",
    "pydantic>=2",
    "sqlalchemy>=2",
    "alembic>=1.11",
]
```

**Config Files:**
- pyproject.toml
- alembic.ini
- .env.example

**Topics**: `fastapi, python, rest-api, uvicorn, pydantic`

### Django + Python

**Structure:**
```
project/
├── project/
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
├── apps/
│   └── users/
├── templates/
├── static/
├── manage.py
└── requirements.txt
```

**Dependencies:**
```txt
django>=4.2
djangorestframework>=3.14
psycopg2-binary>=2.9
celery>=5.3
```

**Topics**: `django, python, rest-api, django-rest-framework, postgresql`

### Go + Gin

**Structure:**
```
cmd/
├── main.go
└── api/
internal/
├── config/
├── handler/
├── middleware/
├── model/
├── repository/
└── service/
pkg/
├── response/
└── error/
go.mod
```

**Topics**: `golang, gin, rest-api, clean-architecture`

## Fullstack Stacks

### T3 Stack (Next.js + tRPC + TypeScript)

**Structure:**
```
src/
├── server/
│   ├── routers/
│   └── trpc.ts
├── pages/
│   ├── api/
│   └── _app.tsx
├── components/
├── styles/
├── utils/
├── env.js
└── next-env.d.ts
prisma/
└── schema.prisma
```

**Key Dependencies:**
```json
{
  "dependencies": {
    "@trpc/server": "^10",
    "@trpc/client": "^10",
    "@trpc/react-query": "^10",
    "@trpc/next": "^10",
    "@tanstack/react-query": "^4",
    "zod": "^3",
    "prisma": "^5"
  }
}
```

**Topics**: `nextjs, trpc, typescript, t3-stack, prisma, tailwind`

### MERN Stack

**Backend Structure:**
```
backend/
├── src/
│   ├── controllers/
│   ├── models/
│   ├── routes/
│   ├── middleware/
│   ├── config/
│   └── index.ts
├── package.json
├── tsconfig.json
└── .env.example
```

**Frontend Structure:**
```
frontend/
├── src/
│   ├── components/
│   ├── pages/
│   ├── context/
│   ├── hooks/
│   ├── services/
│   ├── types/
│   └── App.tsx
├── package.json
└── vite.config.ts
```

**Topics**: `mern, mongodb, express, react, nodejs, rest-api`

### JAMstack (Next.js + Headless CMS)

**Structure:**
```
src/
├── components/
├── lib/
│   └── cms.ts        # Contentful/Sanity/Strapi client
├── pages/
│   └── blog/
├── styles/
└── posts/            # MDX files (if using file-based)
```

**Topics**: `jamstack, nextjs, headless-cms, static-site, ssg`

## DevOps Stacks

### Docker + Docker Compose

**Structure:**
```
Dockerfile
docker-compose.yml
.dockerignore
.docker/
└── entrypoint.sh
```

**docker-compose.yml**:
```yaml
version: '3.8'
services:
  app:
    build: .
    ports:
      - "3000:3000"
    environment:
      - NODE_ENV=production
    depends_on:
      - db
      - redis

  db:
    image: postgres:15
    volumes:
      - postgres_data:/var/lib/postgresql/data

  redis:
    image: redis:7-alpine
```

**Topics**: `docker, docker-compose, containers, devops`

### Kubernetes (K8s)

**Structure:**
```
k8s/
├── base/
│   ├── deployment.yaml
│   ├── service.yaml
│   └── configmap.yaml
├── overlays/
│   ├── dev/
│   ├── staging/
│   └── production/
kustomization.yaml
```

**Topics**: `kubernetes, k8s, kubectl, container-orchestration`

### Terraform + AWS

**Structure:**
```
terraform/
├── modules/
│   ├── ec2/
│   ├── rds/
│   └── s3/
├── environments/
│   ├── dev/
│   └── prod/
├── main.tf
├── variables.tf
└── outputs.tf
```

**Topics**: `terraform, aws, infrastructure-as-code, iac, devops`

## Mobile Stacks

### React Native + Expo

**Structure:**
```
src/
├── components/
├── screens/
├── navigation/
├── hooks/
├── services/
├── types/
├── App.tsx
└── app.json
```

**Topics**: `react-native, expo, mobile, ios, android`

### Flutter

**Structure:**
```
lib/
├── main.dart
├── screens/
├── widgets/
├── providers/
├── models/
├── services/
└── utils/
pubspec.yaml
```

**Topics**: `flutter, dart, mobile, ios, android, cross-platform`

## Data Science Stacks

### Python + ML

**Structure:**
```
notebooks/
├── eda.ipynb
└── modeling.ipynb
src/
├── data/
├── models/
├── features/
├── evaluation/
└── __init__.py
scripts/
├── download_data.py
└── train.py
requirements.txt
pyproject.toml
```

**Dependencies:**
```toml
dependencies = [
    "numpy",
    "pandas",
    "scikit-learn",
    "tensorflow",
    "jupyter",
]
```

**Topics**: `machine-learning, python, data-science, deep-learning, jupyter`

### Apache Spark + Delta Lake

**Structure:**
```
src/
├── etl/
├── transforms/
└── jobs/
notebooks/
├── analysis.ipynb
└── etl.ipynb
spark/
├── config/
└── jars/
dlt_pipeline/
├── bronze/
├── silver/
└── gold/
```

**Topics**: `spark, delta-lake, data-engineering, etl, pyspark`

## Quick Stack Selection Guide

| Project Type | Recommended Stack | Complexity |
|-------------|-------------------|------------|
| Simple API | FastAPI | Low |
| Full Web App | Next.js + Prisma | Medium |
| CLI Tool | Go or Node.js | Low |
| Mobile App | React Native | Medium |
| ML Pipeline | Python + ML libs | High |
| Microservices | Go + Docker | Medium |
| Static Site | Next.js + MDX | Low |
| Real-time App | Node.js + Socket.io | Medium |

When user describes a project, identify keywords to determine the best stack:
- "API", "backend" → FastAPI or Express
- "website", "landing page" → Next.js or Vite + React
- "bot", "automation" → Node.js or Python
- "mobile app" → React Native or Flutter
- "data", "ML", "model" → Python + ML stack
- "infrastructure", "deploy" → Docker + Terraform
