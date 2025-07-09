# YouTube Video Downloader

## Overview

This is a full-stack YouTube video downloader application that allows users to download YouTube videos in MP3 and MP4 formats. The application features a bilingual interface (Arabic/English) with session-based authentication for privacy and security.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

The application follows a modern full-stack architecture with clear separation between client and server:

### Frontend Architecture
- **Framework**: React with TypeScript using Vite as the build tool
- **UI Library**: Shadcn/ui components built on Radix UI primitives
- **Styling**: Tailwind CSS with CSS variables for theming
- **State Management**: TanStack Query (React Query) for server state
- **Routing**: Wouter for lightweight client-side routing
- **Form Handling**: React Hook Form with Zod validation

### Backend Architecture
- **Runtime**: Node.js with Express.js framework
- **Language**: TypeScript with ES modules
- **Database**: PostgreSQL with Drizzle ORM
- **Session Management**: Session-based authentication with unique tokens
- **File Processing**: FFmpeg for video conversion and yt-dlp for YouTube downloads

## Key Components

### Database Schema
The application uses three main database tables:
- **Sessions**: Manages user sessions with unique tokens
- **Videos**: Stores YouTube video metadata (title, thumbnail, duration, etc.)
- **Downloads**: Tracks download requests and their status

### Core Services
- **YouTubeDownloader**: Handles video information extraction and downloading using yt-dlp
- **FileConverter**: Manages audio/video conversion using FFmpeg
- **Storage**: Abstracted storage interface with in-memory implementation

### Authentication & Security
- Session-based authentication using unique tokens (format: TK-XXXXXXXXXXXX)
- No user registration required - anonymous sessions
- Token-based API access for all operations

### Client Components
- **TokenDisplay**: Shows and manages session tokens
- **UrlInput**: YouTube URL validation and submission
- **VideoPreview**: Displays video information and format selection
- **DownloadProgress**: Real-time download progress tracking
- **DownloadHistory**: Lists user's download history

## Data Flow

1. User visits the application and receives a unique session token
2. User enters a YouTube URL which gets validated client-side
3. Server extracts video metadata using yt-dlp
4. User selects download format (MP3/MP4) and initiates download
5. Server processes the download with real-time progress updates
6. Completed downloads are available for immediate download
7. Download history is maintained per session

## External Dependencies

### Core Technologies
- **Database**: PostgreSQL (configured for Neon serverless)
- **Video Processing**: yt-dlp for YouTube downloads
- **Audio/Video Conversion**: FFmpeg for format conversion

### Frontend Libraries
- React ecosystem (React Query, React Hook Form, Wouter)
- Radix UI for accessible components
- Tailwind CSS for styling
- Date-fns for date manipulation

### Backend Libraries
- Express.js for server framework
- Drizzle ORM for database operations
- UUID for session token generation
- Various utility libraries for file handling

## Deployment Strategy

### Development Setup
- Vite dev server for frontend with HMR
- tsx for TypeScript execution in development
- Integrated development experience with file watching

### Production Build
- Frontend: Vite builds to `dist/public`
- Backend: esbuild bundles server code to `dist`
- Single deployment artifact containing both client and server

### Database Management
- Drizzle Kit for schema migrations
- Environment-based database URL configuration
- PostgreSQL dialect with connection pooling support

### Environment Configuration
- Development and production environment separation
- Database URL required via environment variables
- Replit-specific optimizations and error handling

The application is designed to be deployed on platforms like Replit with minimal configuration, requiring only a PostgreSQL database connection string.

## Recent Changes

### January 9, 2025 - YouTube Access Fix
- **Issue**: YouTube was blocking yt-dlp with "Sign in to confirm you're not a bot" errors
- **Solution**: Implemented multi-method approach with fallback strategies:
  - Primary: Web client with proper user-agent headers
  - Fallback 1: Android client with missing token bypass
  - Fallback 2: Basic extraction method
- **Enhancement**: Added bilingual error messages for common YouTube issues
- **Status**: YouTube downloading now works with improved reliability

### System Architecture Updates
- Added robust retry mechanism for YouTube video extraction
- Improved error handling with user-friendly messages in both Arabic and English
- Updated yt-dlp to latest version (2025.6.30) for better compatibility
- Enhanced session management with IP address tracking and user agent logging
- Removed token display from user interface for better privacy
- Fixed download ID undefined error and improved file serving reliability