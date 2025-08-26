# Next.js Restricted Blog Project

## Project Overview

Build a modern web application that functions as a blog with restricted content access. The application uses "Scenes" instead of traditional blog posts, where users can view scene titles publicly but must be logged in to access detailed content.

## Core Entity: Scene

The main content entity with the following attributes:
- `title`: String (max 100 characters)
- `image`: URL string pointing to image file
- `clue`: String (max 500 characters) - detailed content visible only to authenticated users

## Functional Requirements

### Public Access
- **Home Page**: Display a list of all scene titles
- **Public API**: `GET /api/v1/scene` - Returns list of scenes with titles only (no authentication required)
- **Scene Selection**: Users can click on scene titles, but accessing detail requires authentication

### User Authentication & Access
- **User Login**: `/login` - Authentication form for regular users
- **Restricted Content**: After login, users can access scene details
- **Protected API**: `GET /api/v1/scene/<scene_id>` - Returns full scene details (requires JWT authentication)

### Administrator Features
- **Admin Login**: `/admin-login` - Separate authentication form for administrators
- **Dashboard Access**: Post-login redirect to admin dashboard
- **CRUD Operations**: Full Create, Read, Update, Delete functionality for Scene entities
- **Admin Interface**: Web-based dashboard for scene management

## Technical Architecture

### Backend Framework
- **Next.js** with App Router
- API routes for RESTful endpoints
- Server-side rendering and client-side navigation

### Database
- **PostgreSQL** for data persistence
- Scene entity storage with proper indexing
- User and admin credential storage

### Authentication System
- **NextAuth.js** for administrator authentication
- **JWT tokens** for API access control
- Separate authentication flows for users vs administrators
- Session management and protected routes

### Frontend Styling
- **Tailwind CSS** for responsive, modern UI design
- Mobile-first approach
- Clean, blog-like interface

## API Endpoints Specification

### Public Endpoints
```
GET /api/v1/scene
- Description: Fetch list of all scenes (titles only)
- Authentication: None required
- Response: Array of scenes with id and title fields
```

### Protected Endpoints
```
GET /api/v1/scene/<scene_id>
- Description: Fetch complete scene details
- Authentication: JWT token required
- Response: Full scene object with title, image, and clue

POST /api/v1/scene (Admin only)
- Description: Create new scene
- Authentication: Admin JWT required
- Body: { title, image, clue }

PUT /api/v1/scene/<scene_id> (Admin only)
- Description: Update existing scene
- Authentication: Admin JWT required
- Body: { title, image, clue }

DELETE /api/v1/scene/<scene_id> (Admin only)
- Description: Delete scene
- Authentication: Admin JWT required
```

## Page Routes Structure

### Public Routes
- `/` - Home page with scene titles list
- `/login` - User authentication form
- `/admin-login` - Administrator authentication form

### Protected User Routes
- `/scene/[id]` - Scene detail page (requires user authentication)

### Protected Admin Routes
- `/admin/dashboard` - Admin dashboard home
- `/admin/scenes` - Scene management interface
- `/admin/scenes/create` - Create new scene form
- `/admin/scenes/edit/[id]` - Edit existing scene form

## Database Schema

### Scenes Table
```sql
CREATE TABLE scenes (
  id SERIAL PRIMARY KEY,
  title VARCHAR(100) NOT NULL,
  image TEXT NOT NULL,
  clue VARCHAR(500) NOT NULL,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### Users Table (for NextAuth.js)
```sql
CREATE TABLE users (
  id SERIAL PRIMARY KEY,
  email VARCHAR(255) UNIQUE NOT NULL,
  password_hash TEXT NOT NULL,
  role VARCHAR(20) DEFAULT 'user',
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

## Implementation Priorities

1. **Database Setup**: Configure PostgreSQL connection and create initial schema
2. **Authentication System**: Implement NextAuth.js for admin and JWT for users
3. **Public API**: Create unrestricted scene listing endpoint
4. **Home Page**: Build public interface showing scene titles
5. **User Authentication**: Implement user login and JWT token management
6. **Protected Routes**: Create middleware for route protection
7. **Scene Detail Pages**: Build authenticated scene viewing
8. **Admin Authentication**: Implement admin login system
9. **Admin Dashboard**: Create CRUD interface for scene management
10. **API Protection**: Secure admin endpoints with proper JWT validation

## Environment Variables Required

```env
# Database
DATABASE_URL=postgresql://username:password@localhost:5432/blog_db

# NextAuth.js
NEXTAUTH_SECRET=your-secret-key
NEXTAUTH_URL=http://localhost:3000

# JWT for API
JWT_SECRET=your-jwt-secret-key
```

## Security Considerations

- Implement proper JWT token validation for protected endpoints
- Use bcrypt for password hashing
- Add CSRF protection for admin forms
- Validate all input data (length limits for title/clue fields)
- Implement rate limiting on authentication endpoints
- Secure image URL validation to prevent XSS

## UI/UX Requirements

- Responsive design working on mobile and desktop
- Clean, modern blog-like interface
- Clear distinction between public and protected content
- Intuitive admin dashboard with easy CRUD operations
- Loading states and error handling
- Toast notifications for admin actions

## Development Setup Instructions

1. Initialize Next.js project with TypeScript
2. Install required dependencies (NextAuth.js, PostgreSQL client, Tailwind CSS)
3. Set up database connection and run migrations
4. Configure NextAuth.js providers and JWT settings
5. Create API route structure
6. Implement authentication middleware
7. Build component library with Tailwind CSS
8. Test all authentication flows and API endpoints

This project should result in a fully functional, secure blog application with restricted content access and comprehensive admin management capabilities.
