# The Over/Under Machine 

## Overview
The Over/Under Machine is a full-stack web application designed to give sports bettors a statistical edge by automating prop research. Instead of manually cross-referencing player logs and opponent data, this application aggregates historical NBA statistics and calculates the exact probability of a player prop (Over/Under) hitting based on dynamic matchup variables.

## Key Features
* **Probability Engine:** Calculates the historical hit rate of specific Over/Under lines (e.g., Kevin Durant 25.5 Points).
* **Head-to-Head Context:** Instantly retrieves a player's last 5-10 games and historical performance against their current opponent.
* **Advanced Matchup Logic (In Progress):** Factors in Team Pace and Defense vs. Position (DvP) rankings to adjust expected outcomes.
* **Dynamic On/Off Splits (In Progress):** Uses Pandas to filter game logs based on the injury/active status of key teammates.

## Tech Stack
**Frontend (Client)**
* Framework: Next.js / React
* Language: TypeScript
* Styling: Tailwind CSS
* Deployment: Netlify

**Backend (Microservice API)**
* Framework: FastAPI (Python)
* Data Processing: Pandas
* External APIs: `nba_api` (NBA official stats)
* Database: PostgreSQL (for caching player IDs and team data)
* Caching: Redis (to prevent API rate-limiting)
* Deployment: Render / Railway

## System Architecture & Logic
This project utilizes a decoupled, enterprise-grade architecture:
1. **Client Request:** The Next.js frontend sends a search query (Player + Prop Line) to the Python backend.
2. **Data Aggregation:** The FastAPI server checks the Redis cache and PostgreSQL database. If data is stale or missing, it queries the `nba_api` for recent game logs and opponent defensive metrics.
3. **Data Processing:** The backend logic engine processes the JSON payload, calculates the hit rate percentage, applies matchup modifiers, and formats the response.
4. **Client Render:** The frontend receives a clean, lightweight JSON response and renders the probability dashboard for the user.

## Getting Started (Local Development)
*(Instructions on how to run this project locally via Docker will be added here once the MVP is complete).*

## Development Roadmap & Sprint Tracker
*(Note: This section tracks active development sprints and will be removed upon V1.0 launch).*

### Phase 1: Core Data Pipeline (Python/FastAPI)
- [ ] Initialize Python environment and install FastAPI, Uvicorn, and `nba_api`.
- [ ] Build `/api/players/{name}` endpoint to fetch unique NBA Player IDs.
- [ ] Build `/api/stats/{player_id}` endpoint to retrieve raw game logs.
- [ ] Develop the V1 Probability Engine to calculate basic Over/Under hit rates.

### Phase 2: Database & Caching Architecture
- [ ] Set up local PostgreSQL database to cache player metadata.
- [ ] Implement Redis to cache API responses and prevent NBA rate-limiting.
- [ ] Create background task (CRON/APScheduler) to update player data nightly.

### Phase 3: The Client Interface (Next.js)
- [ ] Initialize Next.js, TypeScript, and Tailwind CSS frontend.
- [ ] Build Player Search and Prop Selection UI components.
- [ ] Connect client to FastAPI backend and render the Data Dashboard.

### Phase 4: Advanced Analytics Engine (Pandas)
- [ ] Implement Defense vs. Position (DvP) metric adjustments.
- [ ] Build dynamic On/Off filtering using Pandas (e.g., "Stats without Teammate X").

### Phase 5: Containerization & Deployment
- [ ] Write `docker-compose.yml` to containerize the Frontend, Backend, DB, and Cache.
- [ ] Deploy Next.js frontend to Netlify.
- [ ] Deploy FastAPI backend, PostgreSQL, and Redis to Render/Railway.

### Phase 6: Multi-Sport Scaling (Future Scope)
- [ ] Abstract the database schema to support variable scoring systems.
- [ ] Integrate WNBA data pipelines and positional metrics.
- [ ] Scale engine to support MLB (Pitcher/Batter props) and NHL (Goalie/Skater props).
