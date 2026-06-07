# AGENTS.md

You are building a lightweight Alpine.js application for the Engineer Market Value Scorecard.

Follow `SPEC.md` exactly. The scoring rules in `SPEC.md` are the source of truth.

---

# Project Type

This is a static front-end prototype.

Use:

* Plain HTML
* Alpine.js via CDN
* Tailwind CSS via CDN

Do not use:

* React
* Vue
* Svelte
* npm
* Vite
* Webpack
* Backend code
* Database
* External form services
* Authentication
* API calls

The app must work by opening `index.html` in a browser.

---

# Primary Goal

Build a multi-step wizard that scores software engineer candidates across the framework pillars.

The app should collect answers, calculate pillar scores, calculate the final weighted Candidate Value Score, assign a tier, and show a final report.

---

# Required Wizard Steps

The app must include these steps:

1. Candidate Identity
2. Technical Value Score
3. Interview Readiness Score
4. Branding Score
5. Referral / Recommendation Score
6. PR / Visibility Score
7. Professional Readiness Score
8. Results

Do not add extra scoring categories unless the user asks.

---

# Scoring Pillars

The application must score exactly these six pillars:

1. Technical Value
2. Interview Readiness
3. Branding
4. Referral / Recommendation
5. PR / Visibility
6. Professional Readiness

Each pillar must produce a score from `0–100`.

---

# Pillar Weights

Use these weights exactly:

| Pillar                 | Weight |
| ---------------------- | -----: |
| Technical Value        |    25% |
| Interview Readiness    |    20% |
| Branding               |    15% |
| Referral / Network     |    15% |
| PR / Visibility        |    10% |
| Professional Readiness |    15% |

The final score is the sum of all weighted pillar contributions.

---

# Scoring Rules

Technical Value, Interview Readiness, Branding, Referral / Recommendation, and PR / Visibility use direct point totals. Their selected answers should add up to a maximum of `100`.

Professional Readiness uses Yes/No scoring.

For Professional Readiness:

* Yes = 1
* No = 0
* Score = Yes Answers / Total Questions × 100
* Round to nearest whole number

Do not split Professional Readiness into separate subcategories.

---

# Implementation Requirements

Use an Alpine component named:

```js id="dtpmdu"
candidateScorecard()
```

Keep the code simple and readable.

Use clear state groups:

```js id="u0s05f"
identity
technical
interview
branding
referral
pr
readiness
```

Store questions in editable JavaScript arrays or objects.

Do not hardcode every question manually into repetitive HTML if a loop can render them cleanly.

Keep scoring functions separate from UI rendering.

Use readable function names such as:

```js id="4l97gx"
sumScore()
yesNoScore()
pillarScores
weightedContributions
finalScore
tier
strongestPillar
weakestPillar
recommendation
```

---

# UI Requirements

The UI should be clean, professional, and easy to use.

Use:

* Centered page layout
* Card-based wizard
* Step progress bar
* Step count, such as `Step 2 of 8`
* Clear section titles
* Short section descriptions
* Radio buttons for scored multiple-choice questions
* Yes/No toggles for Professional Readiness
* Back and Next buttons
* Final results dashboard
* Score bars
* Weighted contribution display
* Strongest pillar callout
* Weakest pillar callout
* 30-day recommendation box

Avoid:

* Heavy animations
* Over-designed UI
* Large text blocks inside the app
* Hidden scoring logic
* Unnecessary dependencies

---

# Validation Rules

Keep validation simple.

Candidate Identity required fields:

* Full Name
* Target Role
* Target Level

Scored questions may default to `0`.

Do not block the candidate because of low or incomplete scored answers.

---

# Results Screen Requirements

The Results screen must show:

* Candidate name
* Candidate email, if provided
* Target role
* Target level
* Target market
* Candidate positioning statement, if provided
* Final Candidate Value Score
* Candidate tier
* Candidate tier description
* Pillar-by-pillar score breakdown
* Raw score for each pillar
* Weight for each pillar
* Weighted contribution for each pillar
* Progress bar for each pillar
* Strongest pillar
* Weakest pillar
* Recommended 30-day action plan

---

# Candidate Tiers

Use these tiers exactly:

| Final Score | Tier                       |
| ----------- | -------------------------- |
| 90–100      | Elite Candidate            |
| 75–89       | Strong Candidate           |
| 60–74       | Competitive but Incomplete |
| 40–59       | Underpositioned Candidate  |
| 0–39        | Foundation Stage           |

---

# Recommendation Logic

The recommendation should be based on the weakest pillar.

Use the recommendation text from `SPEC.md`.

Do not invent a different recommendation system unless asked.

---

# File Rules

Preferred file structure:

```txt id="vl1d4o"
engineer-scorecard/
  AGENTS.md
  SPEC.md
  index.html
```

For version one, keep everything inside `index.html`.

Only create `app.js` or `styles.css` if the code becomes difficult to manage.

---

# Quality Standards

The app is complete when:

* The wizard works from start to finish.
* All questions from `SPEC.md` are included.
* Every answer maps to the correct score.
* Each pillar score is calculated correctly.
* The final weighted score is calculated correctly.
* Candidate tier is displayed correctly.
* Strongest and weakest pillars are calculated correctly.
* Recommendation changes based on weakest pillar.
* The app works without build tools.
* The code is easy to edit later.

---

# Important Instruction

Do not change the scoring policy.

Do not rename scoring pillars.

Do not add extra frameworks.

Do not add a backend.

Do not make assumptions that conflict with `SPEC.md`.

When in doubt, preserve the framework exactly as written in `SPEC.md`.

