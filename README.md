# Brand Radar

> 🚀 **[Production Link](https://signalai.atlasprods.com/onboard)** — _This is the live Brand Radar app. Access the production environment here!_


Brand Radar is an AI-powered competitive intelligence platform that transforms LinkedIn data into actionable business insights. It moves beyond traditional analytics dashboards to provide real-time competitive intelligence, AI-generated strategic briefings, and content strategy recommendations.

## Product Overview

Brand Radar scrapes and analyzes LinkedIn posts from companies and their competitors, using advanced LLM processing to extract strategic insights, sentiment analysis, and engagement patterns. The platform provides three core intelligence capabilities:

- **The Pulse**: Real-time competitive intelligence feed that alerts users to competitor activities, viral content, and strategic shifts
- **AI Briefings**: One-click executive summaries that synthesize competitive landscape data into actionable recommendations  
- **Content Co-pilot**: AI-powered content strategy suggestions and post generation based on high-performing themes

## Architecture

### Technology Stack

**Frontend**
- React 18 with TypeScript
- Vite build system
- Tailwind CSS for styling
- Recharts for data visualization
- Socket.io for real-time updates
- Assistant UI for AI chat interface

**Backend**
- Node.js with Express
- TypeScript
- Prisma ORM with PostgreSQL database
- Socket.io for WebSocket connections
- LangChain for LLM orchestration
- Google AI SDK and Anthropic for LLM services

**Infrastructure**
- pnpm workspace monorepo
- PM2 for process management
- PostgreSQL database
- Bright Data for LinkedIn scraping

### Data Flow

1. **Data Ingestion**: LinkedIn posts are scraped and stored as `CompanyPost` records with comprehensive metadata including engagement metrics, hashtags, and media content

2. **Content Analysis**: A multi-stage LLM pipeline processes raw posts:
   - First pass extracts structured data (themes, sentiment, technologies, hiring signals)
   - Second pass generates strategic insights and actionable recommendations
   - Results stored in `PostContentAnalysis` and `StrategicInsight` tables

3. **API Layer**: RESTful APIs serve both standard analytics (engagement, frequency) and AI-enhanced data (strategic insights, content themes)

4. **Frontend Integration**: React components consume analytics APIs through custom hooks, displaying insights across multiple dashboard views

### Database Schema

Core models include:
- `CompanyPost`: LinkedIn post data with engagement metrics and content
- `CompanyProfile`: Company tracking configuration
- `PostContentAnalysis`: LLM-extracted themes, sentiment, and entities
- `StrategicInsight`: High-level strategic recommendations and alerts

## Getting Started

### Prerequisites
- Node.js 18+
- PostgreSQL
- pnpm

### Installation

1. Clone the repository:
```bash
git clone <repository-url>
cd brand-radar
```

2. Install dependencies:
```bash
pnpm install
```

3. Set up the database:
```bash
cd backend
pnpm run db:setup
```

4. Configure environment variables:
```bash
# Backend (.env)
DATABASE_URL=postgresql://user:password@localhost:5432/signal_ai
GOOGLE_API_KEY=your_google_api_key
ANTHROPIC_API_KEY=your_anthropic_api_key

# Frontend (.env)
VITE_BACKEND_URL=http://localhost:3041
```

5. Start development servers:
```bash
# Start both frontend and backend
pnpm run dev

# Or use PM2 for production
pnpm run pm2:start
```

The frontend will be available at `http://localhost:5173` and the backend API at `http://localhost:3041`.

## API Endpoints

### Analytics
- `GET /api/analytics/:profileId/engagement` - Engagement metrics over time
- `GET /api/analytics/:profileId/hashtags` - Top performing hashtags
- `GET /api/analytics/:profileId/top-posts` - Highest engagement posts

### AI Analytics
- `GET /api/ai-analytics/:profileId/themes` - Content themes analysis
- `GET /api/ai-analytics/:profileId/insights` - Strategic insights feed
- `GET /api/ai-analytics/:profileId/events` - Detected events and announcements

### Chat
- `POST /api/chat/query` - Interactive AI chat for data exploration

## Development

The project uses a monorepo structure with shared TypeScript types and utilities:

```
brand-radar/
├── frontend/          # React application
├── backend/           # Express API server
├── packages/shared/   # Shared types and utilities
└── ecosystem.config.js # PM2 configuration
```

### Key Scripts
- `pnpm run dev` - Start development servers
- `pnpm run build` - Build all packages
- `pnpm run pm2:start` - Start with PM2
- `backend: pnpm run db:setup` - Initialize database

## License

This project is proprietary software developed for competitive intelligence purposes.
