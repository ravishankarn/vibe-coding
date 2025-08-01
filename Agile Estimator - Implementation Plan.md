# Agile Estimator MVP – Documentation

## ✅ MVP Overview: Agile Estimator (AI-aided)

### 🎯 Purpose

Help Agile teams estimate story points more consistently using AI-assisted suggestions, based on story text and historical patterns. Goal: Speed up planning and reduce estimation debates.

### 👥 Target Users

* Developers
* Scrum Masters
* Product Owners

### 🧩 Core Features

1. **User Story Input** – Paste or type story text.
2. **AI-Aided Estimation Suggestion** – Rule-based logic for now; AI prompt later.
3. **Team Voting Option (Optional)** – Compare user vote with AI.
4. **Historical View** – Browse past stories and estimates.
5. **Export Planning Session** – JSON or CSV output.

---

## 👥 Team Capacity & Dev Summary

* **Team Size:** 6 developers
* **Total Time:** 3 hours/day × 3 days = 54 person-hours
* **Tools:** GitHub Copilot Business, Node.js, React, Tailwind

### 🏗️ Task Breakdown

| Dev   | Day 1                                         | Day 2                                          | Day 3                   |
| ----- | --------------------------------------------- | ---------------------------------------------- | ----------------------- |
| Dev 1 | Setup repo, folder structure, Tailwind config | Build Story Input Form                         | UI polish, theme        |
| Dev 2 | Build API structure (Express)                 | Implement Estimation Engine (rules or mock AI) | Export logic (JSON/CSV) |
| Dev 3 | Create frontend for suggestion display        | Voting form + comparison view                  | Integration testing     |
| Dev 4 | Build mock data & history panel               | Connect API to UI                              | Bug fixing              |
| Dev 5 | Setup authentication stub (role: dev/PO)      | Add role-based view for PO                     | Demo story loading      |
| Dev 6 | GitHub CI config, Copilot setup               | Write unit tests for estimation logic          | Final bug fixes, deploy |

---

# 📐 System Design

## 🔹 Architecture Overview

```
React (Frontend)
   |
   |-- Axios/Fetch
   |
Node.js + Express (Backend)
   |
   |-- Estimation Engine (Rule-based or AI prompt)
   |-- Historical Data Store (in-memory / JSON file)
```

## 🔹 1. Frontend (React + Tailwind)

### Main Pages:

* `/` — Story Input + Estimation Suggestion
* `/history` — Past story estimates
* `/login` — (optional stub if needed)

### Components:

* `StoryInputForm.tsx`
* `EstimationResult.tsx`
* `VotingPanel.tsx`
* `HistoryPanel.tsx`
* `SessionExport.tsx`

## 🔹 2. Backend (Node.js + Express)

### API Endpoints:

| Method | Endpoint        | Purpose                                      |
| ------ | --------------- | -------------------------------------------- |
| `POST` | `/api/estimate` | Accepts story text, returns suggested points |
| `GET`  | `/api/history`  | Returns mock past stories                    |
| `POST` | `/api/submit`   | Save the final user estimate (for export)    |

### Folder Structure:

```
/backend
  /routes
    estimate.js
    history.js
  /logic
    estimator.js   <-- core estimation logic
  /data
    history.json   <-- mock story dataset
server.js
```

## 🔹 3. Data Structure Examples

### User Story Input

```json
{
  "story": "As a user, I want to upload a file and process it for virus scanning before it's stored."
}
```

### Estimation Output

```json
{
  "suggestedPoint": 5,
  "reasons": ["file upload", "security", "processing logic"]
}
```

---

# 🧠 Estimation Logic Plan

## 🎯 Goal

Suggest a story point based on complexity & scope.

### Option 1: Rule-Based Scoring (MVP-Ready)

#### Steps:

1. Tokenize story into words
2. Match against weighted keyword buckets
3. Add score → map to Fibonacci story point

#### Keyword Buckets:

```js
const rules = {
  "low": ["UI", "button", "text", "label", "copy", "minor", "style"],
  "medium": ["create", "upload", "database", "update", "fetch", "API"],
  "high": ["integrate", "third-party", "auth", "security", "multi-step", "async"],
  "veryHigh": ["migrate", "refactor", "legacy", "compliance", "batch", "real-time"]
};
```

#### Mapping Score → Points:

```js
if (score <= 2) return 1;
if (score <= 5) return 3;
if (score <= 8) return 5;
if (score <= 11) return 8;
return 13;
```

### Option 2: Post-MVP AI Prompt

Use OpenAI prompt:

> "Given the user story below, return a recommended Agile story point estimate (1, 3, 5, 8, or 13) and explain your reasoning."

Input:

> "As a user, I want to integrate with a third-party API to fetch real-time weather updates."

Keyword hits:

* `third-party` → +3
* `API` → +2
* `real-time` → +3
* `fetch` → +2
  ➡️ **Score = 10 → Suggest 8 points**

---

# 📦 Deliverables

* ✅ Hosted MVP (Vercel/Netlify)
* ✅ GitHub repo with:

  * Source code & Copilot-assisted commits
  * Setup instructions & architecture docs
  * Mock story history dataset
* ✅ Exportable planning session (JSON/CSV)

---

Let this serve as your base project documentation. You can copy this into a `README.md`, Confluence, or GitHub Wiki directly.



# 🧠 GitHub Copilot Prompts – Agile Estimator MVP

This document contains GitHub Copilot prompt instructions for each developer over a 3-day sprint to build the Agile Estimator MVP. These prompts are designed to be pasted directly into your working files to help Copilot generate code efficiently.

---

## 👨‍💻 Dev 1: UI Scaffold + Story Input + Styling

### Day 1 Prompt
```tsx
/* 
Create a basic React app layout using Tailwind CSS.
Add a header with the title: 'Agile Estimator'.
Include navigation for 'Home', 'History', and 'Export'.
Main content area should be centered and responsive.
*/
```

### Day 2 Prompt
```tsx
/*
Build a React component named StoryInputForm.
Include a text area where the user can paste a user story.
Add a submit button labeled 'Estimate'.
Use Tailwind CSS for styling.
On submit, send POST to /api/estimate with the story text.
Display the API response below the form.
*/
```

### Day 3 Prompt
```tsx
/*
Add a dark/light mode toggle in the header.
Use Tailwind to adjust theme based on selected mode.
Persist user preference in localStorage.
*/
```

---

## 👨‍💻 Dev 2: Express API + Estimation Logic + Export

### Day 1 Prompt
```ts
/* 
Create an Express.js server with CORS and JSON parsing.
Set up a POST route at /api/estimate that accepts story text in JSON format.
Return a mock response with story points.
*/
```

### Day 2 Prompt
```ts
/*
Write a function estimateStoryPoints(storyText) that:
- Tokenizes the text
- Matches keywords from predefined buckets (low, medium, high)
- Scores the story and maps it to 1, 3, 5, 8, or 13
Return the point value and matching keywords.
*/
```

### Day 3 Prompt
```ts
/*
Add an endpoint /api/export to return all submitted stories and estimates as a downloadable JSON.
Use an in-memory array or simple file-based (history.json) data store.
*/
```

---

## 👨‍💻 Dev 3: Estimation Result + Voting UI

### Day 1 Prompt
```tsx
/*
Create a React component called EstimationResult.
It should take props for story, suggestedPoints, and keywords.
Render the story in a readable card.
Show the suggested points with badge styling.
*/
```

### Day 2 Prompt
```tsx
/*
Build a VotingPanel component.
Allow user to select a story point (1, 3, 5, 8, 13) using radio buttons.
Compare user's vote with the suggested estimate.
Show a summary: 'You selected X, AI suggested Y.'
*/
```

### Day 3 Prompt
```tsx
/*
Add validation to prevent empty vote submission.
If submitted, post data to /api/submit for persistence.
*/
```

---

## 👨‍💻 Dev 4: History Page + Integration

### Day 1 Prompt
```tsx
/*
Create mock JSON file with 10 user stories and their story points.
Each item should have id, storyText, storyPoint, and estimatedBy (AI/human).
*/
```

### Day 2 Prompt
```tsx
/*
Build a HistoryPanel React component.
Fetch data from /api/history.
Display stories in a scrollable table with:
- Story text preview
- Estimated point
- Estimator (AI/User)
*/
```

### Day 3 Prompt
```tsx
/*
Add a filter dropdown to HistoryPanel to filter by story point (1, 3, 5, 8, 13).
Implement client-side filtering only.
*/
```

---

## 👨‍💻 Dev 5: Role-based View + Demo Loader

### Day 1 Prompt
```tsx
/*
Create a simple login stub that allows selecting between roles:
- Developer
- Product Owner
Store selected role in localStorage or context.
Use this role to conditionally render different UI components.
*/
```

### Day 2 Prompt
```tsx
/*
For Product Owner role:
Show a dashboard with the following:
- Total stories estimated today
- Average story point
- List of most frequent keywords in last 5 stories
Use mock data.
*/
```

### Day 3 Prompt
```tsx
/*
Add a button to load a sample story from predefined examples.
On click, autofill the StoryInputForm with sample text.
*/
```

---

## 👨‍💻 Dev 6: GitHub Actions + Tests + Deployment

### Day 1 Prompt
```yaml
# .github/workflows/deploy.yml
# Create a GitHub Action to:
# - Install Node dependencies
# - Run linting and tests
# - Deploy frontend to Vercel or Netlify
```

### Day 2 Prompt
```ts
/*
Write unit tests for estimateStoryPoints() function.
Test edge cases:
- Simple UI change
- Complex integration
- No matching keywords
Use Jest for testing.
*/
```

### Day 3 Prompt
```ts
/*
Run a dry-run deployment to Vercel.
Ensure environment variables (if any) are configured.
Write a README section with setup and deployment steps.
*/
```
