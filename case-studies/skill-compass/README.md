# Skill Compass — Student Career Discovery

**Context:** A college admissions workflow for Class 12 students in India  
**Status:** Preparing for commercial deployment and large-scale use  
**App access and source code:** Private

## Problem

The college's existing Google Forms workflow collected student responses but offered no immediate course guidance. Counselors then had to review spreadsheet responses manually.

I built Skill Compass to turn interest and skill responses into immediate course recommendations and structured data for counselors, with an emphasis on collecting less personal information.

## My contribution

- Built a mobile-friendly quiz using HTML, CSS, and JavaScript, including an animated SVG compass.
- Implemented a multi-factor scoring engine based on interest weights, skill ratings, and tie-breakers.
- Ran scoring in the browser for immediate feedback and on the backend for verification.
- Built a Google Apps Script webhook and Google Sheets dashboards, with serverless fallback support.
- Integrated Gemini Flash through the backend to explain close course matches.
- Added daily AI budget tracking and pre-written fallback notes.
- Built a Node.js local simulator and automated tests with `node:test` and Playwright.

## Recommendation flow

1. A student completes the interest and skill questionnaire.
2. The deterministic engine ranks courses from the configured catalog.
3. The backend verifies submitted scores and records the quiz response.
4. For close matches, the backend can request a short AI comparison using the relevant course information.
5. If the configured daily AI budget is reached, the app provides pre-written guidance.
6. A student can separately opt in to a counselor callback.

The AI explains close matches; it does not determine the course ranking.

## Engineering decisions

### Deterministic matching with limited AI assistance

The scoring rules make rankings repeatable and inspectable. AI is reserved for short comparison notes where additional explanation is useful. Recommendations depend on the quality of the questionnaire, scoring rules, and course catalog.

### Less personal data by default

Students can get results without logging in or providing their name, phone number, or school. Quiz responses are stored with an identifier, while contact details are collected through a separate callback opt-in. Personal contact information is excluded from AI requests.

An identifier alone does not establish full anonymity or legal compliance; the design reduces direct personal-data collection.

### A small, explicit course catalog

For a catalog of approximately 30 degrees, supplying course information in the prompt avoided maintaining a vector database. This reduced infrastructure complexity and constrained the AI's context. Generated notes can still contain errors and should be checked against the catalog.

### Budget tracking and fallback guidance

Backend locking and usage tracking coordinate the configured daily AI allowance. Pre-written notes keep the student flow usable when that allowance is reached. Budget tracking should be described as a cost-control mechanism rather than a guarantee against every possible charge.

### Static frontend deployment

The frontend has no build step and can be hosted as static files. Backend functions retain API credentials and handle verification and AI requests.

### Local testing

The simulator supports testing without cloud credentials. The automated suites exercise application behavior locally and in the browser.

## Deployment plans

Built to replace a form-only admissions workflow with instant course guidance and counselor dashboards. Preparing for commercial deployment and large-scale use.

The project was designed around free-tier hosting and a small frontend payload. AI inference is a separate usage-based cost. Exact timing and cost figures should be published with their measurement conditions, model version, and date.

## Technology

HTML5, CSS3, JavaScript, Google Apps Script, Node.js serverless functions, Google Sheets, Gemini Flash, `node:test`, and Playwright. Supporting storage includes SQLite or a key-value store, depending on the deployment variant.

## Relevance to my career direction

This project demonstrates applied AI through a constrained explanation feature, plus deterministic business logic, backend verification, privacy-conscious data collection, serverless operations, cost controls, and local testing.
