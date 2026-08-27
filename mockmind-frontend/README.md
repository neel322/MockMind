# MockMind Frontend

This directory contains the React and Vite web application for MockMind. It provides account screens, interview setup, the live question-and-answer flow, results, and saved session history.

## Run Locally

From this directory:

```bash
npm install
npm run dev
```

The development server runs at `http://localhost:5173` and expects the FastAPI backend at `http://localhost:8000` by default. To use another backend URL, create `.env.local`:

```env
VITE_API_URL=http://localhost:8000
```

## Commands

```bash
npm run dev      # Start Vite with hot reload
npm run lint     # Check the source with ESLint
npm run build    # Create a production build
npm run preview  # Serve the production build locally
```

See the repository [README](../README.md) for backend setup, environment variables, API endpoints, and the complete application flow.
