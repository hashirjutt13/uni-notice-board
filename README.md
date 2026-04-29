# University Digital Notice Board

A static multi-page website for COMSATS University Islamabad, built with plain HTML and CSS, bundled with **Parcel**, linted with **HTMLHint** and **Stylelint**, and delivered via a fully automated **GitHub Actions CI/CD** pipeline that pushes a production image to **Docker Hub**.

---

## Overview

The COMSATS Digital Notice Board provides students and faculty with a central hub for:

- University announcements and official notices
- Mid-semester and final examination schedules
- Admissions information and important dates
- A contact form to reach university departments

---

## Tech Stack

| Layer | Tool |
|---|---|
| Markup | HTML5 (semantic, HTMLHint-linted) |
| Styling | Vanilla CSS with custom properties |
| Bundler | Parcel v2 |
| HTML Linter | HTMLHint |
| CSS Linter | Stylelint + stylelint-config-standard |
| CI/CD | GitHub Actions |
| Containerisation | Docker (multi-stage build) + Nginx |

---

## Folder Structure

```
uni-notice-board/
├── .github/
│   └── workflows/
│       └── ci.yml          # CI/CD pipeline (lint → build → docker)
├── src/
│   ├── index.html          # Home page
│   ├── notices.html        # Official notices table
│   ├── exams.html          # Exam schedule table
│   ├── admissions.html     # Admissions information
│   └── contact.html        # Contact form + university info
├── styles/
│   └── style.css           # Global stylesheet with CSS variables
├── .dockerignore
├── .gitignore
├── .htmlhintrc             # HTMLHint rules
├── .stylelintrc.json       # Stylelint config
├── Dockerfile              # Multi-stage Docker build
├── package.json
└── README.md
```

---

## Local Development

### Prerequisites

- Node.js 18+
- npm 9+
- Docker Desktop (for container commands)

### Install Dependencies

```bash
npm install
```

### Run Linters

```bash
# Lint all HTML files
npm run lint:html

# Lint all CSS files
npm run lint:css
```

### Start Dev Server

```bash
npm run dev
# Opens http://localhost:1234
```

### Production Build

```bash
npm run build
# Output written to ./dist/
```

### Run with Docker

```bash
# Build the image
docker build -t uni-notice-board .

# Run the container
docker run -p 8080:80 uni-notice-board

# Visit http://localhost:8080
```

---

## CI/CD Pipeline

The GitHub Actions workflow (`.github/workflows/ci.yml`) runs automatically on every push to any branch and on pull requests targeting `develop`.

```
push / pull_request
        │
        ▼
   ┌─────────┐
   │  lint   │  HTMLHint + Stylelint
   └────┬────┘
        │ needs: lint
        ▼
   ┌─────────┐
   │  build  │  Parcel → uploads dist/ artifact
   └────┬────┘
        │ needs: build
        ▼
   ┌─────────┐
   │ docker  │  Downloads artifact → builds image → pushes to Docker Hub
   └─────────┘
```

### Required GitHub Secrets

| Secret | Description |
|---|---|
| `DOCKERHUB_USERNAME` | Your Docker Hub username |
| `DOCKERHUB_TOKEN` | Docker Hub access token |

Add these under **Repository → Settings → Secrets and variables → Actions**.

---

## Team

| Name | Role | Student ID |
|---|---|---|
| Placeholder | Developer | SP26-XXX-XXX |
| Placeholder | Designer | SP26-XXX-XXX |
| Placeholder | DevOps | SP26-XXX-XXX |

---

## Docker Hub

Image available at:

```
docker pull <DOCKERHUB_USERNAME>/uni-notice-board:latest
```

> Replace `<DOCKERHUB_USERNAME>` with your actual Docker Hub username after the first successful CI run.
