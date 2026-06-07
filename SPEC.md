# SPEC.md

# Engineer Market Value Scorecard

## Project Goal

Build a lightweight Alpine.js multi-step wizard that scores software engineer candidates based on the Engineer Market Value Framework.

The application should help a candidate understand how prepared, positioned, visible, and professionally ready they are for FAANG, Fortune 500, and elite technology roles.

The app should collect candidate answers, score each framework category, apply weighted scoring, and show a final Candidate Value Score with a breakdown and recommendation.

---

# Technology Requirements

Use:

* Plain HTML
* Alpine.js via CDN
* Tailwind CSS via CDN

Do not use:

* React
* Vue
* npm
* Vite
* Webpack
* Backend code
* Database
* External form services

The first version should be a static prototype that can run by opening `index.html` in a browser.

---

# File Structure

Use this structure:

```txt
engineer-scorecard/
  AGENTS.md
  SPEC.md
  index.html
```

Optional, only if the file becomes too large:

```txt
engineer-scorecard/
  AGENTS.md
  SPEC.md
  index.html
  app.js
  styles.css
```

For version one, keep everything inside `index.html` unless code organization becomes difficult.

---

# Framework Scoring Categories

The framework is scored across six pillars:

1. Technical Value Score
2. Interview Readiness Score
3. Branding Score
4. Referral / Recommendation Score
5. PR / Visibility Score
6. Professional Readiness Score

Each pillar is scored out of 100.

The final Candidate Value Score is calculated by multiplying each pillar score by its assigned weight, then adding all weighted contributions.

---

# Overall Weighted Scoring

| Pillar                 | Weight |
| ---------------------- | -----: |
| Technical Value        |    25% |
| Interview Readiness    |    20% |
| Branding               |    15% |
| Referral / Network     |    15% |
| PR / Visibility        |    10% |
| Professional Readiness |    15% |
| Total                  |   100% |

## Final Score Formula

```js
finalScore =
  technicalValueScore * 0.25 +
  interviewReadinessScore * 0.20 +
  brandingScore * 0.15 +
  referralRecommendationScore * 0.15 +
  prVisibilityScore * 0.10 +
  professionalReadinessScore * 0.15
```

Round the final score to the nearest whole number for display.

## Weighted Scoring Examples

If a candidate scores `50/100` in Interview Readiness, and Interview Readiness is worth `20%` overall:

```txt
50 × 0.20 = 10
```

So Interview Readiness contributes `10 points` to the final Candidate Value Score.

If a candidate scores `70/100` in Professional Readiness, and Professional Readiness is worth `15%` overall:

```txt
70 × 0.15 = 10.5
```

So Professional Readiness contributes `10.5 points` to the final Candidate Value Score.

If a candidate scores `80/100` in Technical Value, and Technical Value is worth `25%` overall:

```txt
80 × 0.25 = 20
```

So Technical Value contributes `20 points` to the final Candidate Value Score.

The final score is the sum of all weighted pillar contributions.

---

# Candidate Tiers

Use the final weighted score to classify the candidate.

| Final Score | Tier                       |
| ----------- | -------------------------- |
| 90–100      | Elite Candidate            |
| 75–89       | Strong Candidate           |
| 60–74       | Competitive but Incomplete |
| 40–59       | Underpositioned Candidate  |
| 0–39        | Foundation Stage           |

## Tier Descriptions

### Elite Candidate

The candidate is highly positioned and ready to target elite companies. They likely need focused outreach, referrals, and strong interview execution.

### Strong Candidate

The candidate has a strong foundation but may need better visibility, stronger referrals, or sharper interview readiness.

### Competitive but Incomplete

The candidate has real potential but is missing important pieces in proof, presentation, network, or interview readiness.

### Underpositioned Candidate

The candidate may have ability, but their market positioning, proof, or readiness is not strong enough yet.

### Foundation Stage

The candidate needs structured development before seriously targeting elite companies.

---

# Wizard Steps

The app should use a multi-step wizard.

Steps:

1. Candidate Identity
2. Technical Value Score
3. Interview Readiness Score
4. Branding Score
5. Referral / Recommendation Score
6. PR / Visibility Score
7. Professional Readiness Score
8. Results

Each step should include:

* Step title
* Short description
* Questions
* Back button
* Next button
* Progress indicator
* Clear current step count, such as `Step 2 of 8`

The Results step should show the final candidate report.

---

# Step 1: Candidate Identity

This step is not scored. It personalizes the final report.

## Fields

### Full Name

Input type: text
Required: yes

State key:

```js
identity.name
```

### Email

Input type: email
Required: no

State key:

```js
identity.email
```

### Target Role

Input type: select
Required: yes

Options:

* Backend Engineer
* Frontend Engineer
* Full Stack Engineer
* DevOps / Cloud Engineer
* Data Engineer
* AI / ML Engineer
* Mobile Engineer
* Cybersecurity Engineer
* Product Engineer
* Software Engineering Intern
* Not Sure Yet

State key:

```js
identity.targetRole
```

### Target Level

Input type: select
Required: yes

Options:

* Internship
* Entry-Level
* Mid-Level
* Senior
* Staff / Principal
* Not Sure Yet

State key:

```js
identity.targetLevel
```

### Target Market

Input type: checkbox group
Required: no

Options:

* FAANG
* Fortune 500
* AI Startups
* Fintech
* Healthtech
* Enterprise SaaS
* Government / Defense
* Remote Global Companies
* Not Sure Yet

State key:

```js
identity.targetMarket
```

### Candidate Positioning Statement

Input type: textarea
Required: no

Prompt:

```txt
Describe yourself in one sentence as a software engineer.
```

Example:

```txt
Backend engineer focused on scalable APIs, cloud infrastructure, and payment systems.
```

State key:

```js
identity.positioning
```

---

# Step 2: Technical Value Score

This measures actual ability and proof of engineering competence.

Total: 100 points.

| Area                       | Points |
| -------------------------- | -----: |
| Production projects        |     20 |
| Real users / deployment    |     20 |
| Measurable impact          |     20 |
| Open source / GSOC         |     15 |
| Technical depth            |     15 |
| Certifications / academics |     10 |
| Total                      |    100 |

## Question 1: How many production-level projects have you built?

Area: Production projects
Max points: 20

Note:

A production-level project is not just a tutorial or classroom exercise. It should be deployable, usable, documented, and close to a real-world product, tool, feature, or system.

Options:

* 0 projects — 0 points
* 1 project — 5 points
* 2–3 projects — 10 points
* 4–5 projects — 15 points
* 6+ projects — 20 points

State key:

```js
technical.productionProjects
```

## Question 2: Have any of your projects been used by real users?

Area: Real users / deployment
Max points: 20

Note:

Real users prove that the candidate has built something beyond private practice. This includes customers, internal teams, classmates, open-source users, startup users, client users, or public users.

Options:

* No real users — 0 points
* A few users — 5 points
* 100+ users — 10 points
* 1,000+ users — 15 points
* 10,000+ users — 20 points

State key:

```js
technical.realUsers
```

## Question 3: Do you have measurable impact from your work?

Area: Measurable impact
Max points: 20

Note:

Measurable impact can include improved speed, reduced load time, increased revenue, user growth, reduced infrastructure cost, automation, improved uptime, fewer errors, or improved team workflow.

Options:

* No measurable impact — 0 points
* Some claims, but no numbers — 5 points
* At least one measurable result — 10 points
* Multiple measurable results — 15 points
* Strong metrics tied to business or engineering outcomes — 20 points

State key:

```js
technical.measurableImpact
```

## Question 4: Have you contributed to open source or participated in GSOC-style programs?

Area: Open source / GSOC
Max points: 15

Note:

This includes open-source contributions, Google Summer of Code, hackathons, research labs, internships, engineering fellowships, or other structured engineering programs. These signals show collaboration, discipline, public proof, and external validation.

Options:

* No — 0 points
* Minor contribution or participation — 4 points
* Several contributions or completed participation — 8 points
* Regular contributor or strong program completion — 12 points
* Maintainer, winner, recognized contributor, or published participant — 15 points

State key:

```js
technical.openSourceGsoc
```

## Question 5: Can you clearly explain the technical architecture, tradeoffs, and complexity behind your strongest projects?

Area: Technical depth
Max points: 15

Note:

Technical depth measures whether the candidate can explain architecture, tradeoffs, scalability, debugging, performance, security, data modeling, infrastructure, and why certain engineering decisions were made.

Options:

* Weak technical depth — 0 points
* Basic understanding — 4 points
* Can explain common implementation decisions — 8 points
* Can explain architecture and tradeoffs clearly — 12 points
* Strong senior-level technical reasoning — 15 points

State key:

```js
technical.technicalDepth
```

## Question 6: Do you have technical certifications, degrees, diplomas, or academic credentials?

Area: Certifications / academics
Max points: 10

Note:

Certifications and academics do not replace real engineering ability, but they improve credibility and perceived value. This can include degrees, diplomas, bootcamps, technical certificates, cloud certifications, security certifications, AI/data certifications, or relevant coursework.

Options:

* None — 0 points
* Basic online certificates — 2 points
* Degree, diploma, bootcamp, or one respected certification — 5 points
* Multiple respected credentials — 8 points
* Credentials strongly aligned with target role — 10 points

State key:

```js
technical.certificationsAcademics
```

---

# Step 3: Interview Readiness Score

This measures the candidate’s ability to pass actual hiring processes.

Total: 100 points.

| Area                                      | Points |
| ----------------------------------------- | -----: |
| DSA / LeetCode                            |     25 |
| System design                             |     25 |
| Mock interviews                           |     20 |
| Technical communication under pressure    |     15 |
| Number of interview-style problems solved |     15 |
| Total                                     |    100 |

## Question 1: How consistent is your LeetCode / DSA practice?

Area: DSA / LeetCode
Max points: 25

Note:

For FAANG-style and elite technology interviews, algorithmic problem solving is still a major filter. This question measures consistency, not just talent.

Options:

* No practice — 0 points
* Occasional practice — 6 points
* Weekly practice — 12 points
* Several times per week — 18 points
* Structured, consistent practice with strong topic coverage — 25 points

State key:

```js
interview.dsaLeetcode
```

## Question 2: Have you practiced system design?

Area: System design
Max points: 25

Note:

System design measures the ability to reason about scalable architecture, databases, APIs, caching, queues, reliability, performance, and tradeoffs. It is especially important for mid-level, senior, and backend/platform roles.

Options:

* No system design practice — 0 points
* Watched videos only — 6 points
* Practiced basic designs — 12 points
* Can design common systems — 18 points
* Can explain senior-level tradeoffs clearly — 25 points

State key:

```js
interview.systemDesign
```

## Question 3: Have you done mock interviews or interview simulations?

Area: Mock interviews
Max points: 20

Note:

Interview simulation helps candidates practice communication, timing, pressure, and structured thinking. Many candidates know the topic but fail under interview conditions.

Options:

* None — 0 points
* 1–2 mock interviews — 5 points
* 3–5 mock interviews — 10 points
* 6–10 mock interviews — 15 points
* 10+ mock interviews with feedback and improvement — 20 points

State key:

```js
interview.mockInterviews
```

## Question 4: Can you explain your solutions clearly out loud?

Area: Technical communication under pressure
Max points: 15

Note:

This measures whether the candidate can think out loud, explain tradeoffs, clarify assumptions, respond to feedback, and communicate while solving problems.

Options:

* No — 0 points
* Weak — 4 points
* Average — 8 points
* Good — 12 points
* Excellent — 15 points

State key:

```js
interview.technicalCommunication
```

## Question 5: How many interview-style coding problems have you solved?

Area: Number of interview-style problems solved
Max points: 15

Note:

This measures breadth of exposure to interview-style problems. It should not reward quantity alone, but quantity helps indicate preparation depth when paired with understanding.

Options:

* 0–25 problems — 0 points
* 26–75 problems — 4 points
* 76–150 problems — 8 points
* 151–300 problems — 12 points
* 300+ problems — 15 points

State key:

```js
interview.problemCount
```

---

# Step 4: Branding Score

This measures how clearly and professionally the candidate is packaged.

Branding is how well the candidate presents their value through owned assets such as LinkedIn, resume, portfolio, GitHub, and positioning.

Total: 100 points.

| Area                | Points |
| ------------------- | -----: |
| LinkedIn            |     20 |
| Resume              |     20 |
| Portfolio website   |     20 |
| GitHub presentation |     20 |
| Positioning clarity |     20 |
| Total               |    100 |

## Question 1: Do you have an optimized LinkedIn profile?

Area: LinkedIn
Max points: 20

Note:

An optimized LinkedIn profile should clearly communicate target role, technical identity, experience, projects, keywords, credibility, and availability.

Options:

* No LinkedIn — 0 points
* Basic LinkedIn — 5 points
* Updated profile but weak positioning — 10 points
* Strong headline, summary, skills, and experience — 15 points
* Strong profile with recommendations, projects, activity, and clear positioning — 20 points

State key:

```js
branding.linkedin
```

## Question 2: Do you have a polished resume?

Area: Resume
Max points: 20

Note:

A polished resume should be clean, ATS-friendly, impact-based, targeted to the candidate’s role, and saved as a professional PDF.

Options:

* No resume — 0 points
* Basic resume — 5 points
* Updated resume — 10 points
* Strong impact-based resume — 15 points
* Tailored, ATS-tested resume for target roles — 20 points

State key:

```js
branding.resume
```

## Question 3: Do you have a personal website or portfolio?

Area: Portfolio website
Max points: 20

Note:

A portfolio or personal website gives the candidate an owned platform to present projects, case studies, writing, resume, GitHub, contact details, and positioning.

Options:

* No website or portfolio — 0 points
* Basic one-page site — 5 points
* Portfolio with projects — 10 points
* Portfolio with case studies — 15 points
* Strong website with blog, projects, resume, contact, and clear positioning — 20 points

State key:

```js
branding.portfolioWebsite
```

## Question 4: Is your GitHub organized and presentable?

Area: GitHub presentation
Max points: 20

Note:

A strong GitHub should have clean repositories, useful READMEs, pinned projects, meaningful commit history, documentation, and code that supports the candidate’s target role.

Options:

* No GitHub — 0 points
* Has repos but messy — 5 points
* Some clean repos — 10 points
* Good READMEs and pinned projects — 15 points
* Strong GitHub with production-level repos, documentation, and contribution history — 20 points

State key:

```js
branding.githubPresentation
```

## Question 5: Is your positioning consistent across platforms?

Area: Positioning clarity
Max points: 20

Note:

Positioning clarity means the resume, LinkedIn, GitHub, portfolio, bio, and public content all point toward the same professional identity and target market.

Options:

* No consistency — 0 points
* Slight consistency — 5 points
* Somewhat consistent — 10 points
* Mostly consistent — 15 points
* Highly consistent, clear, and memorable — 20 points

State key:

```js
branding.positioningClarity
```

---

# Step 5: Referral / Recommendation Score

This measures access to people who can help the candidate reach opportunities.

Total: 100 points.

| Area                         | Points |
| ---------------------------- | -----: |
| Target-company connections   |     25 |
| Referral readiness           |     25 |
| Recommendations              |     25 |
| Community / network strength |     25 |
| Total                        |    100 |

## Question 1: Do you know engineers working at your target or desired companies?

Area: Target-company connections
Max points: 25

Note:

Connections at target companies increase access to information, referrals, mentorship, and hiring opportunities.

Options:

* No — 0 points
* 1–2 weak connections — 6 points
* Several connections — 12 points
* Strong relationships with some — 18 points
* Multiple strong relationships inside target companies — 25 points

State key:

```js
referral.targetCompanyConnections
```

## Question 2: Do you have people who would refer you?

Area: Referral readiness
Max points: 25

Note:

Referral readiness means the candidate has people who understand their value well enough to refer them confidently.

Options:

* No — 0 points
* Maybe — 6 points
* 1 person — 12 points
* 2–3 people — 18 points
* 4+ people — 25 points

State key:

```js
referral.referralReadiness
```

## Question 3: Do you have written recommendations?

Area: Recommendations
Max points: 25

Note:

Written recommendations improve trust and perceived credibility. These may come from managers, senior engineers, clients, professors, maintainers, mentors, or team leads.

Options:

* None — 0 points
* 1 informal recommendation — 6 points
* 1 written or LinkedIn recommendation — 12 points
* Multiple recommendations — 18 points
* Recommendations from managers, senior engineers, clients, or maintainers — 25 points

State key:

```js
referral.recommendations
```

## Question 4: Are you active in technical communities?

Area: Community / network strength
Max points: 25

Note:

Technical communities can create relationships, referrals, visibility, collaboration, learning, and credibility.

Options:

* No — 0 points
* Passive member — 6 points
* Occasionally active — 12 points
* Regular contributor — 18 points
* Known member, organizer, mentor, or community leader — 25 points

State key:

```js
referral.communityStrength
```

---

# Step 6: PR / Visibility Score

This measures whether the candidate has external exposure and third-party credibility.

PR is different from branding. Branding is how the candidate presents themselves. PR is whether the market sees, mentions, shares, features, or validates the candidate.

Total: 100 points.

| Area                         | Points |
| ---------------------------- | -----: |
| Technical articles / content |     20 |
| Third-party features         |     20 |
| Speaking / interviews        |     20 |
| Community recognition        |     20 |
| Search visibility            |     20 |
| Total                        |    100 |

## Question 1: Have you published technical content?

Area: Technical articles / content
Max points: 20

Note:

Technical content shows that the candidate can communicate ideas, teach, document thinking, and create public proof around their technical identity.

Options:

* No technical content — 0 points
* 1–2 posts — 5 points
* 3–5 posts — 10 points
* 6–10 posts — 15 points
* 10+ strong technical posts — 20 points

State key:

```js
pr.technicalContent
```

## Question 2: Have you appeared on third-party platforms?

Area: Third-party features
Max points: 20

Note:

Third-party platforms include podcasts, interviews, guest blogs, newsletters, YouTube channels, community features, publications, and other platforms not owned by the candidate.

Options:

* No — 0 points
* One minor appearance — 5 points
* A few appearances — 10 points
* Several relevant appearances — 15 points
* Strong third-party credibility — 20 points

State key:

```js
pr.thirdPartyFeatures
```

## Question 3: Have you spoken publicly about technology?

Area: Speaking / interviews
Max points: 20

Note:

Public speaking shows communication skill, confidence, subject matter credibility, and willingness to contribute to the industry.

Examples include meetups, conferences, webinars, workshops, live streams, panels, or events.

Options:

* No — 0 points
* Internal presentation only — 5 points
* Small meetup or informal talk — 10 points
* Webinar, workshop, conference, or event talk — 15 points
* Multiple public talks, workshops, or sessions — 20 points

State key:

```js
pr.speakingInterviews
```

## Question 4: Do others mention, share, recommend, or reference your work?

Area: Community recognition
Max points: 20

Note:

Community recognition means other people validate, share, cite, comment on, recommend, or refer to the candidate’s work.

Options:

* No — 0 points
* A few likes or comments — 5 points
* Some shares or positive mentions — 10 points
* Recognized in a community — 15 points
* Regularly referenced, recommended, or shared — 20 points

State key:

```js
pr.communityRecognition
```

## Question 5: Do you have search visibility?

Area: Search visibility
Max points: 20

Prompt:

When someone searches your name, do credible results appear?

Note:

Search visibility means the candidate has a credible public footprint. This can include LinkedIn, GitHub, personal website, articles, talks, interviews, open-source contributions, or third-party mentions.

Options:

* No relevant results — 0 points
* Only basic social profiles — 5 points
* LinkedIn and personal website appear — 10 points
* Multiple relevant results appear — 15 points
* Strong search presence with external validation — 20 points

State key:

```js
pr.searchVisibility
```

---

# Step 7: Professional Readiness Score

This measures practical readiness, professional presentation, and opportunity preparedness.

Each question carries the same weight and should be scored with Yes or No.

Yes = 1
No = 0

The score should be calculated proportionally based on the number of questions.

Formula:

```txt
Professional Readiness Score = Yes Answers / Total Questions × 100
```

This approach allows the section to grow later by adding more Yes/No questions without changing the scoring structure.

Current total questions: 7

Each Yes answer is worth approximately:

```txt
100 / 7 = 14.2857 points
```

Round the Professional Readiness Score to the nearest whole number.

## Questions

### Question 1: Do you have a professional interview setup?

Note:

A professional interview setup includes a reliable laptop, good camera, clear audio, stable internet, clean background, and proper lighting.

Input type: Yes/No toggle

State key:

```js
readiness.interviewSetup
```

### Question 2: Can you introduce yourself clearly in 30–60 seconds?

Note:

This measures whether the candidate can clearly explain who they are, what they do, and what value they offer. This connects to the “Misc but Important” section of the framework.

Input type: Yes/No toggle

State key:

```js
readiness.selfIntroduction
```

### Question 3: Do you have a professional headshot or profile image?

Note:

A professional image improves trust, consistency, and first impression across LinkedIn, portfolio, GitHub, resume, and other public profiles.

Input type: Yes/No toggle

State key:

```js
readiness.headshot
```

### Question 4: Do you know your target salary range?

Note:

A candidate should know their expected salary range based on role, level, location, company type, and market value.

Input type: Yes/No toggle

State key:

```js
readiness.salaryRange
```

### Question 5: Are your relocation, remote, work authorization, passport, or ID details clear?

Note:

This measures whether the candidate is practically ready to accept opportunities that may require relocation, remote-work clarity, travel, identification, visa information, or work authorization details.

Input type: Yes/No toggle

State key:

```js
readiness.mobilityAuthorization
```

### Question 6: Can recruiters easily contact you?

Note:

Recruiters should be able to reach the candidate through clear channels such as email, LinkedIn, portfolio contact form, phone, or calendar link.

Input type: Yes/No toggle

State key:

```js
readiness.recruiterContact
```

### Question 7: Do you have a target company list?

Note:

A target company list shows that the candidate is not applying randomly. It should include desired companies, company type, priority level, and target roles.

Input type: Yes/No toggle

State key:

```js
readiness.targetCompanyList
```

---

# Results Screen

The Results step should show a full score report.

## Required Output

Show:

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
* Weighted contribution per pillar
* Strongest pillar
* Weakest pillar
* Recommended 30-day action plan

---

# Pillar Breakdown Display

For each pillar, show:

* Pillar name
* Raw score out of 100
* Pillar weight
* Weighted contribution
* Progress bar
* Short interpretation

Example:

```txt
Technical Value: 80/100
Weight: 25%
Contribution: 20 points
```

## Weighted Contribution Formula

For each pillar:

```js
contribution = pillarScore * pillarWeight
```

Example:

```txt
Technical Value score: 80
Technical Value weight: 25%

80 × 0.25 = 20 final-score points
```

---

# Strongest and Weakest Pillar

The app should calculate:

* Strongest pillar = highest raw pillar score
* Weakest pillar = lowest raw pillar score

If multiple pillars tie, return the first one found based on this order:

1. Technical Value
2. Interview Readiness
3. Branding
4. Referral / Recommendation
5. PR / Visibility
6. Professional Readiness

---

# Recommendation Logic

The final 30-day recommendation should be based on the weakest pillar.

## If Technical Value is weakest

Show:

```txt
Focus on building stronger proof of engineering ability. Add one production-quality project, document it clearly, and attach measurable results such as users, performance, automation, revenue, reliability, or cost savings.
```

## If Interview Readiness is weakest

Show:

```txt
Focus on interview execution. Create a 30-day plan for DSA practice, system design practice, mock interviews, and technical communication under pressure.
```

## If Branding is weakest

Show:

```txt
Focus on packaging. Improve your resume, LinkedIn, GitHub, portfolio, and positioning so your target role and technical value are clear within seconds.
```

## If Referral / Recommendation is weakest

Show:

```txt
Focus on access. Build relationships with engineers, recruiters, alumni, open-source maintainers, and people at target companies before asking for referrals.
```

## If PR / Visibility is weakest

Show:

```txt
Focus on visibility. Publish technical content, share project breakdowns, join public technical discussions, and create proof outside your own resume and portfolio.
```

## If Professional Readiness is weakest

Show:

```txt
Focus on professional readiness. Improve your interview setup, self-introduction, profile image, salary clarity, recruiter contactability, work authorization clarity, and target company list.
```

---

# Alpine Component

Use an Alpine component named:

```js
candidateScorecard()
```

---

# Expected Alpine State Shape

Use this general state structure:

```js
{
  currentStep: 1,

  identity: {
    name: '',
    email: '',
    targetRole: '',
    targetLevel: '',
    targetMarket: [],
    positioning: ''
  },

  technical: {
    productionProjects: 0,
    realUsers: 0,
    measurableImpact: 0,
    openSourceGsoc: 0,
    technicalDepth: 0,
    certificationsAcademics: 0
  },

  interview: {
    dsaLeetcode: 0,
    systemDesign: 0,
    mockInterviews: 0,
    technicalCommunication: 0,
    problemCount: 0
  },

  branding: {
    linkedin: 0,
    resume: 0,
    portfolioWebsite: 0,
    githubPresentation: 0,
    positioningClarity: 0
  },

  referral: {
    targetCompanyConnections: 0,
    referralReadiness: 0,
    recommendations: 0,
    communityStrength: 0
  },

  pr: {
    technicalContent: 0,
    thirdPartyFeatures: 0,
    speakingInterviews: 0,
    communityRecognition: 0,
    searchVisibility: 0
  },

  readiness: {
    interviewSetup: false,
    selfIntroduction: false,
    headshot: false,
    salaryRange: false,
    mobilityAuthorization: false,
    recruiterContact: false,
    targetCompanyList: false
  }
}
```

---

# Data Structure Requirement

Questions should be stored in editable JavaScript arrays or objects.

Do not hardcode every question manually into repeated HTML if a loop can render them cleanly.

Recommended structure for scored multiple-choice questions:

```js
{
  id: 'productionProjects',
  label: 'How many production-level projects have you built?',
  note: 'A production-level project is not just a tutorial...',
  maxPoints: 20,
  options: [
    { label: '0 projects', value: 0 },
    { label: '1 project', value: 5 },
    { label: '2–3 projects', value: 10 },
    { label: '4–5 projects', value: 15 },
    { label: '6+ projects', value: 20 }
  ]
}
```

Recommended structure for Yes/No questions:

```js
{
  id: 'interviewSetup',
  label: 'Do you have a professional interview setup?',
  note: 'A professional interview setup includes a reliable laptop...',
}
```

---

# Scoring Functions

## Direct Sum Score

Use this for sections where point values already total 100:

* Technical Value
* Interview Readiness
* Branding
* Referral / Recommendation
* PR / Visibility

```js
sumScore(sectionObject) {
  return Object.values(sectionObject)
    .map(Number)
    .reduce((sum, value) => sum + value, 0);
}
```

## Yes / No Score

Use this for:

* Professional Readiness

```js
yesNoScore(sectionObject) {
  const values = Object.values(sectionObject);
  const yesCount = values.filter(Boolean).length;

  if (!values.length) return 0;

  return Math.round((yesCount / values.length) * 100);
}
```

## Pillar Scores

```js
get pillarScores() {
  return {
    technicalValue: this.sumScore(this.technical),
    interviewReadiness: this.sumScore(this.interview),
    branding: this.sumScore(this.branding),
    referralRecommendation: this.sumScore(this.referral),
    prVisibility: this.sumScore(this.pr),
    professionalReadiness: this.yesNoScore(this.readiness)
  };
}
```

## Pillar Weights

```js
weights: {
  technicalValue: 0.25,
  interviewReadiness: 0.20,
  branding: 0.15,
  referralRecommendation: 0.15,
  prVisibility: 0.10,
  professionalReadiness: 0.15
}
```

## Weighted Contributions

```js
get weightedContributions() {
  const scores = this.pillarScores;

  return {
    technicalValue: scores.technicalValue * this.weights.technicalValue,
    interviewReadiness: scores.interviewReadiness * this.weights.interviewReadiness,
    branding: scores.branding * this.weights.branding,
    referralRecommendation: scores.referralRecommendation * this.weights.referralRecommendation,
    prVisibility: scores.prVisibility * this.weights.prVisibility,
    professionalReadiness: scores.professionalReadiness * this.weights.professionalReadiness
  };
}
```

## Final Score

```js
get finalScore() {
  const contributions = this.weightedContributions;

  const total = Object.values(contributions)
    .reduce((sum, value) => sum + value, 0);

  return Math.round(total);
}
```

## Candidate Tier

```js
get tier() {
  const score = this.finalScore;

  if (score >= 90) return 'Elite Candidate';
  if (score >= 75) return 'Strong Candidate';
  if (score >= 60) return 'Competitive but Incomplete';
  if (score >= 40) return 'Underpositioned Candidate';
  return 'Foundation Stage';
}
```

---

# Validation Rules

Keep validation light for the prototype.

Required fields before moving past Candidate Identity:

* Full Name
* Target Role
* Target Level

For scored question steps:

* Default values can start at `0`.
* Candidate should be able to proceed even if they leave low/default answers.
* Do not block completion because of low scores.

---

# UI Requirements

The UI should feel clean, simple, serious, and professional.

Use:

* Centered layout
* Card-based wizard
* Step progress bar
* Clear labels
* Radio buttons for scored questions
* Yes/No toggles for Professional Readiness
* Back and Next buttons
* Final results dashboard
* Score bars
* Weighted contribution display
* Strongest and weakest pillar callouts
* 30-day recommendation box

Avoid:

* Complicated animations
* Heavy visual effects
* Over-engineering
* Long paragraphs inside the app UI
* Hidden scoring logic

---

# Result Interpretation Text

Use these short interpretations for pillar scores:

## 85–100

```txt
Strong and competitive.
```

## 70–84

```txt
Good foundation with room to improve.
```

## 50–69

```txt
Developing, but incomplete.
```

## 0–49

```txt
Needs focused improvement.
```

---

# Success Criteria

The app is successful when:

* Candidate can complete the multi-step wizard.
* Every question maps to the correct scoring pillar.
* Every scoring section matches the point policy in this spec.
* Technical Value totals 100.
* Interview Readiness totals 100.
* Branding totals 100.
* Referral / Recommendation totals 100.
* PR / Visibility totals 100.
* Professional Readiness is calculated from Yes/No answers.
* Final weighted score is calculated correctly.
* Candidate tier displays correctly.
* Results screen shows raw scores and weighted contributions.
* Strongest and weakest pillars display correctly.
* Recommendation changes based on weakest pillar.
* Code is easy to edit later.

