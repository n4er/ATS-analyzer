# ATS Analyzer

ATS Analyzer is a resume review web app built with React Router, TypeScript, Tailwind CSS, and Puter.js. Users sign in with Puter, upload a PDF resume, paste a target job description, and receive AI-generated feedback with an ATS score plus suggestions for tone, content, structure, and skills.

This version stores uploaded files and analysis results in the user's Puter account, previews the uploaded resume, and keeps a history of analyzed resumes on the home page.

## Features

- Puter-based authentication with no custom backend
- PDF resume upload with drag-and-drop support
- Resume preview generation by converting the PDF to an image
- AI analysis against a job title and job description
- Structured scoring for ATS, tone and style, content, structure, and skills
- Saved resume history using Puter KV storage
- A `/wipe` route for clearing stored Puter app data during testing

## Tech Stack

- React 19
- React Router v7
- TypeScript
- Tailwind CSS v4
- Zustand
- Puter.js
- Vite

## How It Works

1. The app loads Puter.js in the browser.
2. The user signs in with Puter on the auth page.
3. A PDF resume is uploaded to Puter file storage.
4. The PDF is converted to an image for preview.
5. The app sends the resume file and the job details to Puter AI.
6. The AI returns structured JSON feedback that is saved in Puter KV storage.
7. The user can revisit previous resume reviews from the home page.

## Requirements

- Node.js 20 or newer
- npm
- A Puter account
- Internet access, because Puter auth, storage, and AI run through Puter services

## Local Setup

```bash
git clone https://github.com/n4er/ATS-analyzer.git
cd ATS-analyzer
npm install
```

No `.env` file is required for local development in the current setup.

## Run the App

Start the development server:

```bash
npm run dev
```

Then open `http://localhost:5173`.

## Available Scripts

```bash
npm run dev
```

Runs the app in development mode.

```bash
npm run typecheck
```

Generates React Router types and runs TypeScript checks.

```bash
npm run build
```

Builds the client and server bundles for production.

```bash
npm run start
```

Starts the production server from the built output.

## Docker

Build the image:

```bash
docker build -t ats-analyzer .
```

Run the container:

```bash
docker run -p 3000:3000 ats-analyzer
```

Then open `http://localhost:3000`.

## Project Structure

```text
app/
  components/    Reusable UI pieces
  lib/           Puter store, PDF conversion, helpers
  routes/        App routes such as home, auth, upload, resume, and wipe
constants/       Prompt template and shared constants
public/          Static images, icons, and PDF worker
types/           Shared TypeScript types
```

## Notes

- The app currently uses Puter AI with the `anthropic/claude-sonnet-4` model for resume feedback.
- File upload is limited to PDF files up to 20 MB.
- If analysis times out, try a smaller resume file or a shorter job description.
- Uploaded resumes and saved analysis data live in the signed-in user's Puter storage.

## Deployment Checklist

- Install dependencies with `npm install`
- Confirm `npm run typecheck` passes
- Confirm `npm run build` passes
- Make sure the deployed environment can load `https://js.puter.com/v2/`

## License

This project is provided as-is for learning and personal portfolio use unless you add a separate license file.
