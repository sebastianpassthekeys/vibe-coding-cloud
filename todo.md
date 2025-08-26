# Next.js Restricted Blog - Detailed TODO Tasks

## Phase 1: Project Setup & Foundation

### 1.1 Project Initialization
- [ ] Create new Next.js project with TypeScript using `npx create-next-app@latest --typescript --tailwind --eslint --app`
- [ ] Configure `next.config.js` for image optimization and API settings
- [ ] Set up `.env.local` file with required environment variables
- [ ] Initialize Git repository and create `.gitignore`
- [ ] Create basic folder structure (`/components`, `/lib`, `/types`, `/hooks`)

### 1.2 Dependencies Installation
- [ ] Install NextAuth.js: `npm install next-auth`
- [ ] Install PostgreSQL client: `npm install pg @types/pg`
- [ ] Install JWT libraries: `npm install jsonwebtoken @types/jsonwebtoken`
- [ ] Install bcrypt for password hashing: `npm install bcryptjs @types/bcryptjs`
- [ ] Install form validation: `npm install react-hook-form @hookform/resolvers zod`
- [ ] Install UI components: `npm install @headlessui/react @heroicons/react`
- [ ] Install database migration tool: `npm install drizzle-orm drizzle-kit` (or prisma)

## Phase 2: Database Setup

### 2.1 Database Configuration
- [ ] Set up PostgreSQL database locally or cloud instance
- [ ] Create database connection utility in `/lib/db.ts`
- [ ] Test database connection
- [ ] Set up database client configuration

### 2.2 Database Schema Creation
- [ ] Create migration for `scenes` table with proper constraints
- [ ] Create migration for `users` table for NextAuth.js
- [ ] Create migration for `accounts` table (NextAuth.js requirement)
- [ ] Create migration for `sessions` table (NextAuth.js requirement)
- [ ] Run initial migrations
- [ ] Create database seeding script with sample data

### 2.3 Database Models/Types
- [ ] Define TypeScript interfaces for Scene entity
- [ ] Define TypeScript interfaces for User entity
- [ ] Create database query utilities in `/lib/queries/`
- [ ] Create CRUD operations for scenes
- [ ] Create user management operations

## Phase 3: Authentication System

### 3.1 NextAuth.js Configuration
- [ ] Create `/app/api/auth/[...nextauth]/route.ts`
- [ ] Configure NextAuth.js with credentials provider for admins
- [ ] Set up JWT strategy and session configuration
- [ ] Create admin user seeding script
- [ ] Test admin authentication flow

### 3.2 JWT Token Management
- [ ] Create JWT utility functions in `/lib/jwt.ts`
- [ ] Implement token generation for user login
- [ ] Implement token validation middleware
- [ ] Create token refresh mechanism
- [ ] Handle token expiration

### 3.3 Authentication Middleware
- [ ] Create API route protection middleware
- [ ] Create page route protection middleware
- [ ] Implement role-based access control (user vs admin)
- [ ] Create authentication context provider
- [ ] Add authentication state management

## Phase 4: API Routes Implementation

### 4.1 Public API Endpoints
- [ ] Create `GET /api/v1/scene` - public scene list endpoint
- [ ] Implement scene title-only response filtering
- [ ] Add proper error handling and status codes
- [ ] Add request validation
- [ ] Test endpoint functionality

### 4.2 Protected User API Endpoints
- [ ] Create `GET /api/v1/scene/[id]` - protected scene detail endpoint
- [ ] Implement JWT validation middleware
- [ ] Add scene existence validation
- [ ] Handle unauthorized access
- [ ] Test with valid/invalid tokens

### 4.3 User Authentication API
- [ ] Create `POST /api/auth/login` - user login endpoint
- [ ] Implement user credential validation
- [ ] Generate and return JWT tokens
- [ ] Add rate limiting for login attempts
- [ ] Handle login errors and responses

### 4.4 Admin CRUD API Endpoints
- [ ] Create `POST /api/v1/scene` - create scene (admin only)
- [ ] Create `PUT /api/v1/scene/[id]` - update scene (admin only)
- [ ] Create `DELETE /api/v1/scene/[id]` - delete scene (admin only)
- [ ] Implement admin role validation
- [ ] Add input validation and sanitization
- [ ] Test all CRUD operations

## Phase 5: Frontend Pages & Components

### 5.1 Layout and Common Components
- [ ] Create main layout component with navigation
- [ ] Create header component with authentication status
- [ ] Create footer component
- [ ] Create loading spinner component
- [ ] Create error message component
- [ ] Create toast notification component

### 5.2 Public Pages
- [ ] Create home page (`/app/page.tsx`) - display scene titles list
- [ ] Implement scene titles fetching from public API
- [ ] Add responsive grid layout for scene titles
- [ ] Create scene title card component
- [ ] Handle loading and error states
- [ ] Add click handlers for scene selection

### 5.3 User Authentication Pages
- [ ] Create user login page (`/app/login/page.tsx`)
- [ ] Create login form component with validation
- [ ] Implement login submission and JWT handling
- [ ] Add password visibility toggle
- [ ] Handle login errors and success messages
- [ ] Add redirect after successful login

### 5.4 Protected User Pages
- [ ] Create scene detail page (`/app/scene/[id]/page.tsx`)
- [ ] Implement authentication check middleware
- [ ] Fetch scene details from protected API
- [ ] Create scene detail component layout
- [ ] Add image display with proper optimization
- [ ] Handle unauthorized access redirects

### 5.5 Admin Authentication Page
- [ ] Create admin login page (`/app/admin-login/page.tsx`)
- [ ] Create admin-specific login form
- [ ] Implement NextAuth.js signIn functionality
- [ ] Add admin role validation
- [ ] Handle admin login errors
- [ ] Redirect to dashboard after successful login

### 5.6 Admin Dashboard Pages
- [ ] Create dashboard layout (`/app/admin/layout.tsx`)
- [ ] Create dashboard home page (`/app/admin/dashboard/page.tsx`)
- [ ] Create scenes management page (`/app/admin/scenes/page.tsx`)
- [ ] Create scene creation page (`/app/admin/scenes/create/page.tsx`)
- [ ] Create scene edit page (`/app/admin/scenes/edit/[id]/page.tsx`)
- [ ] Add admin navigation menu component

### 5.7 Admin CRUD Components
- [ ] Create scene list component with actions (edit, delete)
- [ ] Create scene form component (create/edit)
- [ ] Implement form validation with proper error messages
- [ ] Add image upload/URL input handling
- [ ] Create delete confirmation modal
- [ ] Add success/error notifications for CRUD operations

## Phase 6: Security & Validation

### 6.1 Input Validation
- [ ] Create Zod schemas for scene validation (title max 100, clue max 500)
- [ ] Create Zod schemas for user login validation
- [ ] Implement server-side validation for all API routes
- [ ] Add client-side form validation
- [ ] Sanitize user inputs to prevent XSS

### 6.2 Security Measures
- [ ] Implement CSRF protection for admin forms
- [ ] Add rate limiting for authentication endpoints
- [ ] Validate image URLs to prevent malicious content
- [ ] Add password strength requirements
- [ ] Implement secure session management
- [ ] Add security headers configuration

### 6.3 Error Handling
- [ ] Create global error boundary component
- [ ] Implement consistent API error responses
- [ ] Add proper 404 pages for missing scenes
- [ ] Handle database connection errors
- [ ] Add authentication error handling

## Phase 7: UI/UX Polish

### 7.1 Responsive Design
- [ ] Ensure all pages work on mobile devices
- [ ] Test tablet and desktop layouts
- [ ] Add proper breakpoints for different screen sizes
- [ ] Optimize image loading for different devices

### 7.2 User Experience
- [ ] Add loading states for all data fetching
- [ ] Implement skeleton loaders
- [ ] Add smooth transitions and animations
- [ ] Create proper focus management for accessibility
- [ ] Add keyboard navigation support

### 7.3 Visual Design
- [ ] Create consistent color scheme and typography
- [ ] Design scene card components with hover effects
- [ ] Style form components with proper error states
- [ ] Add icons for better visual hierarchy
- [ ] Create dark/light theme support (optional)

## Phase 8: Testing & Optimization

### 8.1 Testing
- [ ] Write unit tests for utility functions
- [ ] Test API endpoints with different scenarios
- [ ] Test authentication flows (user and admin)
- [ ] Test CRUD operations thoroughly
- [ ] Perform cross-browser testing

### 8.2 Performance Optimization
- [ ] Optimize image loading and caching
- [ ] Implement proper data caching strategies
- [ ] Minimize bundle size and remove unused dependencies
- [ ] Add SEO optimization for public pages
- [ ] Test and optimize database query performance

### 8.3 Security Audit
- [ ] Review all authentication and authorization flows
- [ ] Test for common security vulnerabilities
- [ ] Validate all input sanitization
- [ ] Check for exposed sensitive information
- [ ] Review JWT token security

## Phase 9: Deployment Preparation

### 9.1 Environment Configuration
- [ ] Set up production environment variables
- [ ] Configure database for production
- [ ] Set up proper CORS settings
- [ ] Configure Next.js for production deployment

### 9.2 Documentation
- [ ] Create deployment guide
- [ ] Document API endpoints
- [ ] Create user manual for admin dashboard
- [ ] Add troubleshooting guide

### 9.3 Final Testing
- [ ] Perform end-to-end testing in production-like environment
- [ ] Test all user flows from start to finish
- [ ] Verify all security measures are working
- [ ] Check performance metrics
