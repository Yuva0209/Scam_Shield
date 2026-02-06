# FraudGuard - UPI Fraud Detection Dashboard

## Overview

FraudGuard is a full-stack fraud detection dashboard designed to identify mule accounts and collusive fraud in UPI (Unified Payments Interface) transactions. The application enables users to upload transaction CSV data, processes it for fraud analysis, and visualizes suspicious patterns through interactive dashboards including network graphs, behavioral DNA radar charts, and risk clustering views.

The system is built for a hackathon focused on detecting fraudulent financial activity patterns such as mule accounts (accounts used to launder money), collusive fraud rings, and suspicious device/behavioral anomalies.

## User Preferences

Preferred communication style: Simple, everyday language.

## System Architecture

### Frontend Architecture
- **Framework**: React 18 with TypeScript
- **Routing**: Wouter (lightweight React router)
- **State Management**: TanStack React Query for server state caching and synchronization
- **UI Components**: shadcn/ui component library built on Radix UI primitives
- **Styling**: Tailwind CSS with custom CSS variables for theming (light/dark mode support)
- **Visualization Libraries**:
  - Recharts for statistical charts (pie charts, bar charts, radar charts)
  - react-force-graph-2d for network graph visualization of fraud relationships
- **Build Tool**: Vite with React plugin

### Backend Architecture
- **Runtime**: Node.js with Express.js
- **Language**: TypeScript (ESM modules)
- **API Design**: RESTful endpoints defined in `shared/routes.ts` with Zod validation schemas
- **File Handling**: Multer for CSV file uploads with memory storage
- **CSV Processing**: csv-parse library for parsing uploaded transaction data

### Data Layer
- **Database**: PostgreSQL
- **ORM**: Drizzle ORM with drizzle-zod for schema validation
- **Schema Location**: `shared/schema.ts` contains all table definitions
- **Key Tables**:
  - `datasets`: Metadata about uploaded CSV files
  - `transactions`: Raw UPI transaction records
  - `deviceLogs`: Device fingerprint and session data
  - `upiProfiles`: Derived behavioral analysis per UPI account (risk scores, roles)
  - `fraudAlerts`: Detected fraud clusters and alerts

### Project Structure
```
├── client/               # React frontend
│   └── src/
│       ├── components/   # Reusable UI components
│       ├── pages/        # Route-based page components
│       ├── hooks/        # Custom React hooks (data fetching)
│       └── lib/          # Utilities and query client
├── server/               # Express backend
│   ├── routes.ts         # API endpoint handlers
│   ├── storage.ts        # Database access layer
│   └── db.ts             # Database connection
├── shared/               # Shared between frontend/backend
│   ├── schema.ts         # Drizzle table definitions
│   └── routes.ts         # API contract definitions
└── migrations/           # Database migrations (Drizzle Kit)
```

### Key Design Patterns
- **Shared Types**: Schema and route definitions in `/shared` ensure type safety between frontend and backend
- **Storage Interface**: `IStorage` interface in `storage.ts` abstracts database operations for testability
- **Component Architecture**: Atomic design with reusable shadcn/ui components in `components/ui/`

## External Dependencies

### Database
- **PostgreSQL**: Primary data store, connection via `DATABASE_URL` environment variable
- **Drizzle Kit**: Database schema migrations (`npm run db:push`)

### Third-Party Libraries (Key Ones)
- **@tanstack/react-query**: Async state management for API calls
- **drizzle-orm / drizzle-zod**: Type-safe ORM with Zod schema generation
- **csv-parse**: Server-side CSV parsing for transaction data uploads
- **react-force-graph-2d**: Interactive force-directed graph for visualizing fraud networks
- **recharts**: Charting library for dashboard visualizations
- **multer**: Multipart form data handling for file uploads
- **zod**: Runtime schema validation for API inputs/outputs



### Environment Variables Required
- `DATABASE_URL`: PostgreSQL connection string (required for database operations)

## Getting Started

1. Install dependencies:
   ```bash
   npm install
   ```

2. Set up the database:
   - Ensure PostgreSQL is running
   - Set the `DATABASE_URL` environment variable
   - Run database migrations:
     ```bash
     npm run db:push
     ```

3. Start the development server:
   ```bash
   npm run dev
   ```

4. Build for production:
   ```bash
   npm run build
   npm start
   ```

## Usage

- Upload CSV files containing UPI transaction data
- View fraud analysis dashboards
- Explore network graphs of suspicious transactions
- Monitor risk scores and behavioral patterns
