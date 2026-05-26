
# FitTrack

FitTrack is an AI-powered fitness and nutrition platform designed to help users plan workouts, track meals, monitor progress, and stay consistent with a clean dashboard experience. It combines a React frontend, a TypeScript/Express backend, PostgreSQL persistence, and Gemini AI generation for personalized fitness and diet plans.

Live Demo: [https://fit-track-v0hp.onrender.com](https://fit-track-v0hp.onrender.com)

Author: [![GitHub](https://img.shields.io/badge/GitHub-Ankush--0g-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/Ankush-0g)

## What FitTrack Does

- Personalized fitness and diet plan generation
- Workout session logging and meal logging
- Progress tracking with charts and stats
- Authentication with onboarding flow
- Admin dashboard for operational visibility
- Gemini AI fallback handling when remote generation is unavailable

## Tech Stack

### Frontend

<p>
    <img src="https://img.shields.io/badge/React-61DAFB?style=for-the-badge&logo=react&logoColor=black" alt="React" />
    <img src="https://img.shields.io/badge/TypeScript-3178C6?style=for-the-badge&logo=typescript&logoColor=white" alt="TypeScript" />
    <img src="https://img.shields.io/badge/Vite-646CFF?style=for-the-badge&logo=vite&logoColor=white" alt="Vite" />
    <img src="https://img.shields.io/badge/Tailwind_CSS-38B2AC?style=for-the-badge&logo=tailwind-css&logoColor=white" alt="Tailwind CSS" />
    <img src="https://img.shields.io/badge/Motion-000000?style=for-the-badge&logo=framer&logoColor=white" alt="Motion" />
    <img src="https://img.shields.io/badge/Lucide-222222?style=for-the-badge&logo=lucide&logoColor=white" alt="Lucide React" />
    <img src="https://img.shields.io/badge/Recharts-8884FF?style=for-the-badge&logo=recharts&logoColor=white" alt="Recharts" />
</p>

### Backend

<p>
    <img src="https://img.shields.io/badge/Node.js-339933?style=for-the-badge&logo=nodedotjs&logoColor=white" alt="Node.js" />
    <img src="https://img.shields.io/badge/Express-000000?style=for-the-badge&logo=express&logoColor=white" alt="Express" />
    <img src="https://img.shields.io/badge/PostgreSQL-4169E1?style=for-the-badge&logo=postgresql&logoColor=white" alt="PostgreSQL" />
    <img src="https://img.shields.io/badge/JWT-000000?style=for-the-badge&logo=jsonwebtokens&logoColor=white" alt="JWT" />
    <img src="https://img.shields.io/badge/bcryptjs-2B579A?style=for-the-badge&logo=securityscorecard&logoColor=white" alt="bcryptjs" />
    <img src="https://img.shields.io/badge/dotenv-ECD53F?style=for-the-badge&logo=dotenv&logoColor=black" alt="dotenv" />
    <img src="https://img.shields.io/badge/Gemini_AI-4285F4?style=for-the-badge&logo=google&logoColor=white" alt="Gemini AI" />
</p>

## System Workflow

```mermaid
flowchart TD
    A[User opens FitTrack] --> B[React frontend]
    B --> C{Authenticated?}
    C -- No --> D[Landing / Auth screens]
    C -- Yes --> E[Onboarding if profile incomplete]
    E --> F[Dashboard]
    D --> G[Login or Register]
    G --> F
    F --> H[Request workout or diet plan]
    H --> I[Express backend API]
    I --> J{Gemini API available?}
    J -- Yes --> K[Generate personalized AI plan]
    J -- No --> L[Use local fallback plan]
    K --> M[Store / return plan data]
    L --> M
    M --> N[PostgreSQL database]
    N --> O[Render cards, charts, logs, and progress]
```

## Project Architecture

FitTrack follows a layered full-stack architecture:

- Presentation layer: React pages and reusable UI components in `src/`
- State and context layer: authentication and theme providers in `src/context/`
- API layer: Express server in `server.ts` handling auth, profile updates, plan generation, and data retrieval
- Service layer: Gemini prompt builders, AI fallback logic, and request orchestration in `server/`
- Data layer: PostgreSQL tables for users, plans, logs, progress, and admin activity

### Core Structure

- `src/pages/` contains the main user screens such as dashboard, onboarding, fitness, diet, progress, and admin views
- `src/components/` contains the reusable UI blocks such as cards, charts, calendar controls, toggles, and logging panels
- `server/` contains database setup, prompt generation, and offline fallback logic
- `server.ts` boots the API, initializes the database, and connects the frontend to backend services

## Gemini AI Integration

FitTrack uses Gemini AI to generate personalized fitness and nutrition content based on the user profile, goals, equipment, and activity data.

- Fitness plan generation is handled through prompt-driven JSON responses
- Diet plan generation creates meal plans with calorie and macro targets
- If the Gemini key is missing, invalid, blocked, or unavailable, FitTrack falls back to local program generation so the app still works
- The backend expects `GEMINI_API_KEY` in the environment and uses the Gemini model configured in the server

## Local Development

### Prerequisites

- Node.js
- PostgreSQL database access if you want to run with your own database
- Gemini API key

### Setup

1. Install dependencies:

```bash
npm install
```

2. Create a `.env.local` file and set the required values:

```bash
GEMINI_API_KEY=your_gemini_api_key
DATABASE_URL=your_postgres_connection_string
JWT_SECRET=your_jwt_secret
```

3. Start the app:

```bash
npm run dev
```

## Build And Run

```bash
npm run build
npm start
```

## Notes

- The app includes authentication, onboarding, admin views, and workout/diet tracking flows.
- Database tables are initialized automatically on startup.
- If Gemini is unavailable, the UI still remains usable through fallback content.
