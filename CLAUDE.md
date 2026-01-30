# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Eventum Backend is a **Strapi v5.11.3** headless CMS application providing REST APIs for content management.

## Development Commands

```bash
npm run develop    # Start dev server with auto-reload (http://localhost:1337)
npm run build      # Build admin panel for production
npm run start      # Start production server (no auto-reload)
npm run deploy     # Deploy to Strapi Cloud
```

## Environment Setup

Copy `.env.example` to `.env` and configure:
- `DATABASE_URL` - PostgreSQL connection string (required for development)
- `APP_KEYS` - Encryption keys (comma-separated)
- `JWT_SECRET` - API JWT secret
- `ADMIN_JWT_SECRET` - Admin panel JWT secret
- Cloudinary credentials for file uploads: `CLOUDINARY_NAME`, `CLOUDINARY_KEY`, `CLOUDINARY_SECRET`

## Architecture

**Database:** PostgreSQL in development (via `DATABASE_URL`), SQLite as fallback. Config at `config/database.ts` with environment override at `config/env/development/database.ts`.

**Key Configuration Files:**
- `config/server.ts` - Host, port, proxy settings
- `config/plugins.ts` - Plugin configuration (Users-Permissions, Cloudinary upload)
- `config/middlewares.ts` - Middleware stack (CORS, security, body parsing)
- `config/api.ts` - REST API settings (default limit: 25, max: 100)

**Entry Points:**
- `src/index.ts` - Application lifecycle hooks (`register()` for pre-init, `bootstrap()` for post-init)
- `src/api/` - Custom API controllers and routes
- `src/extensions/` - Core Strapi functionality extensions

**Plugins:**
- Users-Permissions: JWT authentication and role management
- Upload: Cloudinary-based file storage
- Health: Health check endpoint
