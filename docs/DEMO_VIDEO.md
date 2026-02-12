# Demo Video Guide

## Video Recording Checklist

### 1. Introduction (30 seconds)

- [ ] Introduce yourself
- [ ] State project title: "Multi-Tenant SaaS Platform - Project & Task Management"
- [ ] Brief overview: "A production-ready platform where multiple organizations can independently manage their teams, projects, and tasks with complete data isolation"

### 2. Architecture Walkthrough (2 minutes)

- [ ] Show system architecture diagram from `docs/images/system-architecture.png`
- [ ] Explain Docker containerization (3 containers: database, backend, frontend)
- [ ] Show database ERD from `docs/images/database-erd.png`
- [ ] Explain multi-tenancy approach: Shared Database + Shared Schema with tenant_id isolation
- [ ] Show technology stack:
  - Frontend: React 18 with Vite
  - Backend: Node.js with Express.js - Database: PostgreSQL 15
  - Authentication: JWT
  - Deployment: Docker Compose

### 3. Running the Application (1 minute)

- [ ] Show terminal running `docker-compose up -d`
- [ ] Verify health check: `curl http://localhost:5000/api/health`
- [ ] Show docker ps output (all 3 containers running)
- [ ] Open browser to http://localhost:3000

### 4. Multi-Tenancy Demonstration (3 minutes)

#### 4.1 Tenant Registration

- [ ] Navigate to registration page
- [ ] Fill out form:
  - Organization Name: "Test Company"
  - Subdomain: "test"
  - Admin Email: "admin@test.com"
  - Admin Full Name: "Test Admin"
  - Password: "Test@123"
  - Check Terms & Conditions
- [ ] Submit and show success message
- [ ] Redirect to login

#### 4.2 Tenant Admin Login & Dashboard

- [ ] Login as: admin@demo.com / Demo@123 (subdomain: demo)
- [ ] Show dashboard with statistics:
  - Total Projects
  - Total Tasks
  - Pending Tasks
  - Active Projects
- [ ] Show navigation: Dashboard, Projects, Team Members

### 5. User Management (2 minutes)

- [ ] Navigate to Team Members page
- [ ] Show existing users list
- [ ] Add new user:
  - Email: "developer@demo.com"
  - Full Name: "Developer User"
  - Password: "Dev@123"
  - Role: User
- [ ] Show user added successfully
- [ ] Show user in users list
- [ ] Demonstrate subscription limit (if applicable)

### 6. Project & Task Management (3 minutes)

#### 6.1 Create Project

- [ ] Navigate to Projects page
- [ ] Click "Create New Project"
- [ ] Fill form:
  - Name: "Mobile App Development"
  - Description: "React Native mobile application"
  - Status: Active
- [ ] Submit and show project created

#### 6.2 Add Tasks

- [ ] Click on newly created project
- [ ] Add task:
  - Title: "Design Login Screen"
  - Description: "Create UI mockups"
  - Assign to: Developer User
  - Priority: High
  - Due Date: Next week
- [ ] Show task in list
- [ Update task status: Todo → In Progress
- [ ] Show status change reflected

#### 6.3 Task Filtering

- [ ] Filter tasks by status
- [ ] Filter tasks by priority
- [ ] Search tasks by title

### 7. Data Isolation Demonstration (2 minutes)

- [ ] Logout from demo tenant
- [ ] Login as different tenant (show registration or use test tenant)
- [ ] Show completely different data:
  - Different projects
  - Different users
  - Different tasks
- [ ] Explain: "Each tenant's data is completely isolated using tenant_id filtering"

### 8. Super Admin Dashboard (1 minute)

- [ ] Logout and login as: superadmin@system.com / Admin@123 (no subdomain)
- [ ] Show Super Admin Dashboard:
  - List of all tenants
  - Subscription plans
  - Total users per tenant
  - Total projects per tenant
- [ ] Explain: "Super Admin can view all tenants but doesn't belong to any tenant"

### 9. Code Walkthrough (2-3 minutes)

#### 9.1 Show Project Structure

- [ ] Open VS Code/editor
- [ ] Show backend structure:
  ```
  backend/
    src/
      controllers/   ← API logic
      middleware/    ← Auth, tenant isolation
      routes/        ← API endpoints
    migrations/      ← Database schema
    seeds/           ← Seed data
  ```
- [ ] Show frontend structure:
  ```
  frontend/
    src/
      pages/         ← React pages
      components/    ← Reusable components
      context/       ← Auth context
      api/           ← API client
  ```

#### 9.2 Show Key Code Snippets

- [ ] Open `backend/src/middleware/auth.js` - show JWT validation
- [ ] Open `backend/src/controllers/projectController.js` - show tenant_id filtering:
  ```javascript
  const { tenantId } = req.user;
  const result = await pool.query(
    "SELECT * FROM projects WHERE tenant_id = $1",
    [tenantId],
  );
  ```
- [ ] Explain: "Every query is filtered by tenant_id from JWT token"

#### 9.3 Show Database Schema

- [ ] Open `backend/migrations/001_init.sql`
- [ ] Highlight:
  - tenants table
  - users table with tenant_id foreign key
  - projects table with tenant_id
  - tasks table with tenant_id
  - Audit logs table
- [ ] Show indexes on tenant_id for performance

### 10. Docker Configuration (1 minute)

- [ ] Show `docker-compose.yml`:
  - Database service (port 5432)
  - Backend service (port 5000)
  - Frontend service (port 3000)
- [ ] Show `backend/Dockerfile`:
  - Node.js 18 Alpine base image
  - Migration and seed scripts
  - Health check endpoint
- [ ] Explain automatic database initialization

### 11. Conclusion (30 seconds)

- [ ] Summarize key features:
  - ✅ Complete tenant isolation
  - ✅ Role-based access control
  - ✅ Subscription management
  - ✅ Docker containerization
  - ✅ 20 REST API endpoints
  - ✅ Production-ready security
- [ ] Thank the viewer
- [ ] Provide GitHub repository link

## Recording Tips

- Use screen recording software (OBS Studio, Camtasia, or Zoom)
- Record in 1080p resolution
- Use clear audio (external microphone recommended)
- Edit out long pauses or errors
- Add cursor highlighting for code walkthrough
- Keep video under 12 minutes
- Upload to YouTube as Unlisted or Public

## Test Credentials for Demo

- **Super Admin**: superadmin@system.com / Admin@123 (no subdomain)
- **Tenant Admin**: admin@demo.com / Demo@123 (subdomain: demo)
- **Regular User 1**: user1@demo.com / User@123 (subdomain: demo)
- **Regular User 2**: user2@demo.com / User@123 (subdomain: demo)

## YouTube Upload

1. Title: "Multi-Tenant SaaS Platform - Project & Task Management System"
2. Description:

   ```
   A production-ready multi-tenant SaaS application built with React, Node.js, PostgreSQL, and Docker.

   Features:
   - Complete tenant data isolation
   - JWT authentication with role-based access
   - Project and task management
   - Subscription plan management
   - Dockerized deployment

   Tech Stack: React 18, Node.js, Express.js, PostgreSQL 15, Docker

   GitHub Repository: [Your Repo Link]
   ```

3. Tags: SaaS, Multi-Tenant, React, Node.js, PostgreSQL, Docker, JWT, Project Management
4. Visibility: Unlisted or Public
5. Add link to README.md after upload
