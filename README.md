# MockMind

MockMind is a full-stack AI-powered mock interview platform. Candidates can start a quick interview for a target role or upload a PDF resume so MockMind can extract skills, projects, experience, and education before generating tailored technical questions.

## Features

- Email/password signup and login with JWT authentication
- Resume PDF parsing with skill, project, education, and experience extraction
- AI-generated technical questions using Google Gemini
- Easy, medium, hard, and random difficulty options
- Five, ten, or fifteen question interview sessions
- Answer evaluation with per-question feedback, an overall score, improvement areas, and confidence scoring
- MongoDB-backed interview history with detailed session views
- React frontend with protected routes and browser-based speech input support

## Project Structure

```text
MockMind/
├── mockmind-backend/       # FastAPI API, auth, resume parsing, Gemini, MongoDB
├── mockmind-frontend/      # React + Vite web application
└── README.md
```

## Requirements

- Python 3.10 or newer
- Node.js 18 or newer and npm
- A running MongoDB instance
- A Google Gemini API key

## Configuration

Create `mockmind-backend/.env` locally. Never commit this file or place real credentials in the repository.

```env
MONGO_URI=mongodb://localhost:27017
DB_NAME=mockmind
JWT_SECRET=replace-with-a-long-random-secret
JWT_EXPIRE_HOURS=72
GEMINI_API_KEY=your-gemini-api-key
```

The backend loads these values with `python-dotenv`. The root `.gitignore` ignores `.env` files across the whole project while allowing a future `.env.example` template to be committed.

## Backend Setup

From the repository root:

```bash
cd mockmind-backend
python -m venv .venv
```

Activate the virtual environment:

```bash
# Windows PowerShell
.venv\Scripts\Activate.ps1

# macOS/Linux
source .venv/bin/activate
```

Install dependencies and start the API:

```bash
pip install -r requirement.txt
uvicorn main:app --reload
```

The API runs at `http://localhost:8000`. Interactive API documentation is available at `http://localhost:8000/docs`.

## Frontend Setup

In a second terminal:

```bash
cd mockmind-frontend
npm install
npm run dev
```

The Vite development server runs at `http://localhost:5173`. By default, the frontend calls the backend at `http://localhost:8000`. To use another API URL, create `mockmind-frontend/.env.local`:

```env
VITE_API_URL=http://localhost:8000
```

Available frontend commands:

```bash
npm run dev      # Start the development server
npm run build    # Create a production build
npm run lint     # Run ESLint
npm run preview  # Preview the production build locally
```

## API Overview

All interview and resume endpoints require a bearer token returned by signup or login.

| Method | Endpoint | Purpose |
| --- | --- | --- |
| `POST` | `/auth/signup` | Create an account |
| `POST` | `/auth/login` | Authenticate a user |
| `POST` | `/resume/parse` | Parse an uploaded PDF resume |
| `POST` | `/interview/generate` | Generate interview questions |
| `POST` | `/interview/evaluate` | Evaluate submitted answers and save the session |
| `GET` | `/interview/history` | List the signed-in user's sessions |
| `GET` | `/interview/history/{session_id}` | Get one saved session |

## Typical Flow

1. Start MongoDB and configure the backend `.env` file.
2. Run the FastAPI backend.
3. Run the Vite frontend.
4. Create an account or log in.
5. Choose Resume Mode or Quick Start Mode and configure the session.
6. Answer the generated questions and submit the session.
7. Review the score and feedback, then revisit sessions from Interview History.

## Notes

- Resume uploads must be text-based PDF files; scanned PDFs without a text layer are rejected.
- Gemini is used for question generation and answer evaluation, so a valid API key and network access are required for those workflows.
- CORS is currently configured for the local frontend at `http://localhost:5173`.
