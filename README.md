## Installation

### Prerequisites
- Node.js 18+
- Docker & Docker Compose
- npm or yarn

### 1. Clone the Repository
```bash
git clone <your-repo-url>
cd pilzkraft-shop
```

### 2. Install Backend (Medusa)
```bash
# Create new Medusa backend
npx create-medusa-app@latest

# This will prompt you for:
# - Project name: backend
# - Starter template: (choose your preference)
# - Database: PostgreSQL
# - Admin installation: Yes

# Or create backend only
cd backend
npm init medusa-app

# Install dependencies if needed
npm install

# Run migrations
npm run migrate

# Seed database (optional)
npm run seed

# Start development server
npm run dev
```

### 3. Admin Dashboard

**Option 1: Built-in Admin (Recommended)**
The admin is automatically included with Medusa. Access it at:
```
http://localhost:9000/app
```

**Option 2: Separate Admin Installation**
```bash
# Clone Medusa admin repository
git clone https://github.com/medusajs/admin.git admin

cd admin
npm install

# Create .env file
cat > .env << EOF
GATSBY_STORE_URL=http://localhost:9000
GATSBY_ADMIN_URL=http://localhost:7000
EOF

# Start admin
npm run develop
```

### 4. Install Storefront

**Option A: Next.js Storefront (Recommended)**
```bash
# Use Medusa's Next.js starter
npx create-next-app@latest storefront -e https://github.com/medusajs/nextjs-starter-medusa

cd storefront
npm install

# Create .env.local
cat > .env.local << EOF
NEXT_PUBLIC_MEDUSA_BACKEND_URL=http://localhost:9000
NEXT_PUBLIC_BASE_URL=http://localhost:8000
EOF

npm run dev
```

**Option B: Gatsby Storefront**
```bash
# Clone Medusa Gatsby starter
git clone https://github.com/medusajs/gatsby-starter-medusa.git storefront

cd storefront
npm install

# Create .env
cat > .env << EOF
GATSBY_MEDUSA_BACKEND_URL=http://localhost:9000
EOF

npm run develop
```

### 5. Using Docker (Development)
```bash
# Build and start all services
docker-compose up --build

# Start in detached mode
docker-compose up -d

# View logs
docker-compose logs -f

# Stop all services
docker-compose down

# Remove all containers and volumes
docker-compose down -v

# Rebuild specific service
docker-compose build backend
docker-compose up backend
```

### Access Points
- **Backend API**: http://localhost:9000
- **Admin Dashboard**: http://localhost:9000/app (built-in) or http://localhost:7000 (standalone)
- **Storefront**: http://localhost:8000

### Default Credentials
After seeding the database:
- **Email**: admin@medusa-test.com
- **Password**: supersecret

### Environment Variables

**backend/.env**
```env
DATABASE_URL=postgres://postgres:postgres@localhost:5432/medusa
REDIS_URL=redis://localhost:6379
JWT_SECRET=something-secret
COOKIE_SECRET=something-secret
PORT=9000
NODE_ENV=development
```

**admin/.env** (if using standalone)
```env
GATSBY_STORE_URL=http://localhost:9000
GATSBY_ADMIN_URL=http://localhost:7000
```

**storefront/.env.local** (Next.js)
```env
NEXT_PUBLIC_MEDUSA_BACKEND_URL=http://localhost:9000
NEXT_PUBLIC_BASE_URL=http://localhost:8000
REVALIDATE_SECRET=supersecret
```

**storefront/.env** (Gatsby)
```env
GATSBY_MEDUSA_BACKEND_URL=http://localhost:9000
GATSBY_STORE_URL=http://localhost:8000
```

### Quick Start with Docker
```bash
# Clone repository
git clone <your-repo-url>
cd pilzkraft-shop

# Start all services
docker-compose up -d

# Wait for services to be ready, then run migrations
docker-compose exec backend npm run migrate

# Seed the database (optional)
docker-compose exec backend npm run seed

# Check logs
docker-compose logs -f
```

### Troubleshooting

**Reset database**
```bash
docker-compose down -v
docker-compose up -d postgres redis
sleep 5
docker-compose up -d backend
docker-compose exec backend npm run migrate
docker-compose exec backend npm run seed
```

**Rebuild containers**
```bash
docker-compose down
docker-compose build --no-cache
docker-compose up