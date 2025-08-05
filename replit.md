# Overview

GENIUS.AI is a comprehensive contract optimization platform that leverages artificial intelligence to analyze, evaluate, and optimize German consumer contracts. The system focuses primarily on energy (electricity and gas), telecommunications (internet and mobile), and insurance contracts. The platform automates the entire process from document upload through OCR text extraction, AI-powered analysis with GPT-4, market comparison, and actionable optimization recommendations to help users save money and time.

# User Preferences

Preferred communication style: Simple, everyday language.

# System Architecture

## Frontend Architecture

The frontend is built as a modern React SPA using TypeScript with Vite as the build tool. The architecture follows a component-based approach with shadcn/ui providing a comprehensive design system built on Radix UI primitives and Tailwind CSS for styling.

**Key Frontend Decisions:**
- **React with TypeScript**: Provides type safety and modern development experience
- **Vite**: Fast development server and optimized production builds
- **Wouter**: Lightweight client-side routing solution
- **TanStack React Query**: Server state management with caching, background updates, and error handling
- **shadcn/ui + Radix UI**: Accessible, customizable component library with consistent design tokens
- **Tailwind CSS**: Utility-first styling with custom CSS variables for theming

The frontend implements a dashboard-driven interface with real-time file upload progress, interactive contract management, and an integrated chatbot for user assistance.

## Backend Architecture

The backend follows a RESTful Express.js architecture with TypeScript, implementing a layered service pattern for separation of concerns.

**Core Backend Components:**
- **Express.js Server**: Main application server with middleware for logging, error handling, and file uploads
- **Service Layer**: Modular services for AI analysis, OCR processing, email notifications, and contract management  
- **Storage Layer**: Database abstraction with Drizzle ORM providing type-safe database operations
- **Authentication**: Replit OIDC integration with session-based authentication using express-session

**Key Backend Decisions:**
- **Drizzle ORM**: Type-safe database operations with schema-first approach
- **Service Pattern**: Clean separation between business logic (services) and data access (storage)
- **Multer**: File upload handling with memory storage and type validation
- **Session-based Auth**: Secure authentication using PostgreSQL session store

## Data Storage Architecture

The system uses PostgreSQL as the primary database with a well-structured schema supporting user management, contract storage, and auxiliary features.

**Database Schema Design:**
- **Users Table**: Core user data with plan-based access control (starter, professional, enterprise)
- **Contracts Table**: Comprehensive contract storage with JSON fields for AI analysis results and optimization suggestions
- **Support Tables**: Newsletter subscriptions, chat messages, email notifications, and session storage
- **Audit Trail**: Created/updated timestamps and user association for all major entities

The schema supports flexible JSON storage for AI analysis results while maintaining relational integrity for core business data.

## AI and OCR Integration

**OCR Processing:**
- **Tesseract.js**: Client-side OCR for German text extraction with custom character whitelisting
- **Multi-format Support**: PDF and image file processing with file type validation
- **Progress Tracking**: Real-time upload and processing status updates

**AI Analysis Pipeline:**
- **OpenAI GPT-4**: Contract analysis, key term extraction, risk assessment, and optimization scoring
- **Structured Output**: JSON-formatted analysis results for consistent data processing
- **Market Comparison**: Real-time pricing analysis against German market averages
- **Recommendation Engine**: Actionable suggestions with switching guidance and cost projections

## External Service Integrations

**Email Services:**
- **Nodemailer**: SMTP-based email delivery for notifications and reminders
- **Automated Reminders**: Cancellation date notifications and optimization alerts
- **Template System**: HTML email templates with branded styling

**Check24 Partner Program Integration:**
- **Affiliate Tracking**: Check24 partner ID integration for commission tracking
- **Dynamic URL Generation**: Context-aware tracking URLs for energy, telecom, and insurance comparisons
- **Click Analytics**: User interaction tracking for optimization performance metrics
- **Revenue Optimization**: Automated affiliate link injection in optimization recommendations

**File Processing:**
- **Memory-based Upload**: Efficient file handling without disk storage
- **Type Validation**: MIME type checking for security and compatibility
- **Size Limits**: 10MB file size restriction for performance

**Authentication Integration:**
- **Replit OIDC**: Seamless integration with Replit's authentication system
- **Session Management**: PostgreSQL-backed session storage with configurable TTL
- **User Profile Sync**: Automatic user data synchronization from OIDC claims