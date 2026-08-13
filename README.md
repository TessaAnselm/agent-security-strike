# Agent Security Strike

A dependency-free, timed browser game inspired by the [OWASP Agentic Skills Top 10](https://owasp.org/www-project-agentic-skills-top-10/). It teaches players to recognize security failures across agent permissions, skill installation, dependencies, external instructions, isolation, and scanning.

## What is this game?

This is a timed cybersecurity game about AI agents.

An AI agent is a program that can perform tasks for someone, such as reading emails, searching documents, installing tools, or updating files. The danger is that an agent might be tricked into doing something unsafe or try to do something it was never allowed to do.

For every question, the player sees what an AI agent wants to do and chooses one response:

- **ALLOW** — the action is safe and properly authorized.
- **ASK FOR CONSENT** — a person or security reviewer should approve it first.
- **BLOCK** — the action is dangerous or breaks a security rule.

Players have 30 seconds for each question. Faster correct answers earn more points: an answer with 30 seconds remaining earns 300 speed points, while an answer with 5 seconds remaining earns 50. Correct answers in a row also build a streak bonus. Questions appear in a random order, and the best scores appear on a 24-hour local leaderboard.

The scenarios teach players to recognize malicious AI extensions, compromised software updates, excessive permissions, hidden instructions, weak security sandboxes, and missing human oversight.

The main lesson is simple: **an AI agent should only access what it needs, follow trusted instructions, and ask a human before making risky decisions.**

## Learning guide

See [SCENARIO_GUIDE.md](SCENARIO_GUIDE.md) for a plain-language explanation of every challenge, its correct decision, OWASP category, and security lesson.

## Run locally

From this folder:

```bash
python3 -m http.server 8000
```

Then open `http://localhost:8000`. No install, API key, backend, or database is required. The soundtrack starts after the player begins the challenge and can be muted from the header.

Music: “Typography” by Infraction, provided through [Uppbeat](https://uppbeat.io/t/infraction/typography), license code `FZUFFQUJLKGZQUEH`.

Correct and incorrect answer effects are generated locally with the browser Web Audio API and do not require additional sound files.

## Publish with GitHub and Netlify

This repository is configured for a no-build Netlify deployment through `netlify.toml`. Netlify publishes the repository root and applies production security and caching headers automatically.

### 1. Push to GitHub

Create an empty GitHub repository without adding a generated README or `.gitignore`, then run:

```bash
git add .
git commit -m "Initial Agent Security Strike release"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/YOUR-REPOSITORY.git
git push -u origin main
```

Replace the example repository URL with the URL GitHub provides. Do not commit account tokens or other credentials.

### 2. Connect Netlify

1. In Netlify, choose **Add new project** and **Import an existing project**.
2. Select GitHub and authorize access to the repository.
3. Select this repository.
4. Netlify should read `netlify.toml` automatically. The build command stays empty and the publish directory is `.`.
5. Deploy the site.

Later pushes to `main` will trigger new Netlify deploys automatically. The current leaderboard remains local to each player's browser; a trusted shared competition leaderboard requires server-side scoring and storage.

## Deployment and competition security

This game can be deployed to Netlify as a static site using the included `netlify.toml`. That setup is suitable for demonstrations, classrooms, workshops, and casual competitions where the results do not need to be tamper-resistant.

### Critical competition concerns

The current game runs entirely in the browser and therefore has important trust limitations:

- Answers are visible in `app.js`.
- Players can change `score`, `timeLeft`, and `streak` using browser developer tools.
- The timer runs entirely in the browser and can be paused or modified.
- `localStorage` leaderboard entries can be edited manually.
- Every browser has a separate leaderboard, so there is no authoritative shared ranking.
- Player handles do not prove identity; competitors can reuse another player's name.
- Refreshing the page or opening multiple tabs allows unlimited attempts.
- Question shuffling uses `Math.random()`, which is appropriate for casual play but is not secure randomness.

These limitations are not vulnerabilities that expose a server or user account because the current project has no backend, authentication system, or sensitive data. They are competition-integrity risks: players can manipulate locally calculated results.

OWASP recommends treating security-relevant client values as untrusted and recalculating them on a trusted server. Browser storage must not be treated as an authorization mechanism or authoritative state. See the [OWASP Business Logic Security Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Business_Logic_Security_Cheat_Sheet.html) and [OWASP HTML5 Security Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/HTML5_Security_Cheat_Sheet.html).

For a prize-based, public, or remote competition, use a backend to:

- Keep correct answers out of the browser bundle.
- Record question start and submission times server-side.
- Calculate scores and streaks server-side.
- Accept each question response only once.
- Authenticate players or issue unique competition codes.
- Limit attempts and apply rate limiting.
- Store one shared, authoritative leaderboard.

Netlify can continue hosting the frontend. A secure competition version could add Netlify Functions for server-side validation and a persistent database or managed storage service for the leaderboard.

## Gameplay

Enter a player handle and play through a freshly shuffled question order on every run. Decide whether each agent action should be:

- **ALLOW** — the action satisfies its permissions and security constraints.
- **ASK FOR CONSENT** — explicit human review or approval is required.
- **BLOCK** — the action violates delegation, provenance, scope, integrity, or runtime policy.

Each mission has a 30-second clock. Correct answers earn 10 points for every second remaining, so answering immediately is worth up to 300 points. Consecutive correct answers also earn an increasing 15-point streak bonus. A correct answer after the timer reaches zero earns no speed points. The five best runs are stored in the browser's local storage and ranked by score, then completion time. Each result automatically expires 24 hours after it was recorded.

## OWASP coverage

The expanded challenge set includes all ten categories:

- AST01 — Malicious Skills
- AST02 — Supply Chain Compromise
- AST03 — Over-Privileged Skills
- AST04 — Insecure Metadata
- AST05 — Untrusted External Instructions
- AST06 — Weak Isolation
- AST07 — Update Drift
- AST08 — Poor Scanning
- AST09 — No Governance
- AST10 — Cross-Platform Reuse

Other missions reinforce identity, delegated authorization, scope, consent, expiry, origin restrictions, and high-impact actions.

This is an educational simulation, not a security scanner or enforcement engine. OWASP is referenced as the source framework; this project is not an official OWASP product.

## Files

- `index.html` — game UI
- `styles.css` — styling and animations
- `app.js` — missions, timer, scoring, and local leaderboard
- `SCENARIO_GUIDE.md` — plain-language challenge explanations and answers
