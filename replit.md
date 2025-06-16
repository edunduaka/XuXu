# Xuxu - Group Savings Platform

## Overview

Xuxu is a web application that enables group savings and financial collaboration. It's built with React on the frontend and Express.js on the backend, using PostgreSQL (via Drizzle ORM) for data storage. The application follows a modern architecture with a RESTful API backend and a React-based frontend.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

Xuxu follows a monolithic architecture with separated client and server directories:

1. **Frontend**: React application using Vite as the build tool and bundler
2. **Backend**: Express.js API server providing RESTful endpoints
3. **Database**: PostgreSQL with Drizzle ORM for database operations
4. **Styling**: Tailwind CSS with shadcn/ui components

The application is organized with a clear separation between frontend and backend code:
- `/client`: Contains the React application
- `/server`: Contains the Express.js server
- `/shared`: Contains shared TypeScript interfaces and schemas

## Key Components

### Frontend

1. **React Components**:
   - UI Components: Built on shadcn/ui, which uses Radix UI primitives
   - Layout Components: Header, Footer
   - Registration Components: Form, ProgressSteps, FeatureHighlights, Testimonials

2. **State Management**:
   - React Query for server state
   - React Hook Form for form state and validation
   - Zod for schema validation

3. **Routing**: Using Wouter for lightweight client-side routing

### Backend

1. **Express.js Server**:
   - API routes for user registration
   - File upload handling with Multer
   - Database access layer

2. **Database Layer**:
   - Drizzle ORM for database interactions
   - PostgreSQL as the database (via NeonDB serverless)

3. **Authentication/Authorization**:
   - Schema defined for user management
   - ID document upload capability

## Data Flow

1. **User Registration Flow**:
   - User fills out registration form in a step-by-step process
   - Form data is validated on the client using Zod
   - Form data is submitted to the server, including ID document upload
   - Server validates data and stores in the database
   - Confirmation is sent back to client

2. **Database Operations**:
   - Drizzle ORM handles database queries
   - Schema defined in `shared/schema.ts`
   - Storage interface provides abstraction over database operations

## External Dependencies

### Frontend Dependencies
- React and React DOM for UI rendering
- TanStack Query (React Query) for data fetching
- Radix UI components for accessible UI elements
- Tailwind CSS for styling
- Wouter for routing
- React Hook Form for form handling
- Zod for schema validation

### Backend Dependencies
- Express.js for API server
- Drizzle ORM for database operations
- NeonDB serverless PostgreSQL client
- Multer for file uploads

## Deployment Strategy

The application is configured for deployment on Replit:

1. **Development Mode**:
   - Use `npm run dev` to start the development server
   - This uses Vite's dev server for the frontend with HMR
   - Backend runs with tsx for TypeScript execution

2. **Production Build**:
   - Use `npm run build` to compile frontend and backend
   - Frontend: Vite builds static assets
   - Backend: esbuild bundles the server code
   - Output directory is `dist/`

3. **Production Startup**:
   - Use `npm run start` to run the production build
   - Server serves the static frontend assets
   - API endpoints are available at `/api/*`

## Database Schema

The database schema includes:

```typescript
// User model
export const users = pgTable("users", {
  id: serial("id").primaryKey(),
  firstName: text("first_name").notNull(),
  lastName: text("last_name").notNull(),
  email: text("email").notNull().unique(),
  dateOfBirth: date("date_of_birth").notNull(),
  gender: text("gender").notNull(),
  country: text("country").notNull(),
  state: text("state").notNull(),
  city: text("city").notNull(),
  address1: text("address1").notNull(),
  address2: text("address2"),
  idType: text("id_type").notNull(),
  idDocumentPath: text("id_document_path"),
  createdAt: timestamp("created_at").defaultNow().notNull(),
});
```

## Future Development Areas

1. **Authentication System**:
   - JWT or session-based authentication
   - User login functionality

2. **Group Savings Features**:
   - Creation of savings groups
   - Contribution tracking
   - Goal setting

3. **Payment Integration**:
   - Integration with payment gateways
   - Transaction handling

4. **User Dashboard**:
   - Profile management
   - Savings tracking
   - Analytics

## Development Guidelines

1. **Directory Structure**:
   - Place new React components in the appropriate subdirectories under `client/src/components/`
   - Place new API routes in `server/routes.ts`
   - Place shared types and schemas in `shared/`

2. **Styling Approach**:
   - Use Tailwind CSS utility classes
   - Use shadcn/ui components
   - Follow the established design system

3. **Code Style**:
   - Use TypeScript for type safety
   - Use ESLint and Prettier for code formatting
   - Follow the React Hooks pattern for component state