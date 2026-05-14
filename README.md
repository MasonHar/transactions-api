# transactions-api

REST API for credit card transactions using Node.js, Express, and MongoDB. Local development uses Docker and a VS Code Dev Container.

## Data model

Each transaction includes `creditCardNickname`, `cardType`, `date`, `amount`, `amendment`, and `comment`. The API is append-only (no PUT, PATCH, or DELETE).

## Setup

1. Copy `.env` and set:

   - `PORT=3000`
   - `MONGODB_URI` — local Docker: `mongodb://db:27017/transactionsdb`; production: your Atlas URI with database name in the path (for example `.../transactionsdb`).

2. Install dependencies:

   ```bash
   npm install
   ```

## Run locally

```bash
npm run dev
```

Seed sample data:

```bash
npm run seed
```

## API

| Method | Path | Description |
|--------|------|-------------|
| GET | `/` | Health message |
| POST | `/transactions` | Create a transaction |
| GET | `/transactions` | List (optional query: `date`, `startDate`, `endDate`, `creditCardNickname`) |
| GET | `/transactions/:id` | Get one by MongoDB `_id` |

## Docker

```bash
docker compose up --build
```

## Dev container

Open the folder in **Visual Studio Code**, then use **Dev Containers: Reopen in Container** so the app and MongoDB run in Compose.

## Heroku

- `Procfile` runs `web: node server.js`.
- Set `MONGODB_URI` on the app: `heroku config:set MONGODB_URI="..."`.
- Deploy: `git push heroku main` (from your machine, not inside the container).
