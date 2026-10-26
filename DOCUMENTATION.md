# GitTogether — Comprehensive Project Documentation

**Project Name:** GitTogether  
**Version:** 0.2.0  
**Repository:** [https://github.com/Nareshaspire/gittogether-diff](https://github.com/Nareshaspire/gittogether-diff)  
**Hackathon:** Devpost: Build With AI Basics Hackathon  
**License:** MIT  

---

## 1. Executive Summary

**GitTogether** transforms raw git diffs, pull requests, and code snippets into actionable architectural intelligence in seconds. By coupling real-time AI reasoning with client-side visual line and intra-line diffing, it delivers:
1. **Interactive Visual Diff**: Line-level unified diff with intra-line word-level highlights and syntax coloring.
2. **Automated SemVer Recommendation**: Classification into `Major`, `Minor`, or `Patch` bumps based on breaking change severity.
3. **Plain-English Executive Summary**: High-level synopsis of the modification.
4. **Architectural Blast Radius**: Analysis of module boundaries, data flows, external dependencies, and runtime performance.
5. **Breaking Change Radar**: Categorized severity flags (`High`, `Medium`, `Low`) detailing affected callers and migration steps.
6. **Publish-Ready Markdown Release Notes**: Keep-a-Changelog formatted release notes with one-click copy and `.md` file download.
7. **Direct GitHub PR Ingestion**: Paste any public GitHub PR or commit URL to fetch and inspect multi-file diffs.
8. **Real-Time Streaming**: Server-Sent Events (SSE) streaming with a terminal inspector for live AI reasoning.

---

## 2. Problem Statement & Value Proposition

### The Problem
Reviewing pull requests is one of the highest-cognitive-load activities in software engineering:
- **Subtle Breaking Changes**: Altered parameter orders, type narrowing, or new error-throwing behaviors often escape human review under deadline pressure.
- **Architectural Blast Radius**: Reviewers struggle to trace how changes in a single function ripple across downstream modules, caching layers, or database queries.
- **Tedious Release Documentation**: Writing clean, structured release notes and changelogs is manual, slow, and frequently neglected.

### The Solution
GitTogether acts as an automated, senior reviewer that pairs with engineers. Instead of a passive visual diff, GitTogether synthesizes code changes into structured engineering insights instantly.

---

## 3. System Architecture & Technical Design

### Architectural Diagram
```
+-------------------------------------------------------------------------+
|                          Browser Client (SPA)                           |
|  - Vanilla HTML5 / CSS3 / ES6+ (Zero external UI dependencies)         |
|  - Client-side LCS Diff Engine with intra-line word-level token pairing |
|  - Live SSE Terminal Stream Reader (ReadableStream API)                 |
|  - GitHub Multi-File PR Chip Navigator                                  |
+--------------------+--------------------------------+-------------------+
                     |                                |
        POST /api/analyze (SSE/JSON)      POST /api/github {url}
                     |                                |
+--------------------+--------------------------------+-------------------+
|                     Node.js HTTP Server (server.js)                    |
|  - Zero runtime npm dependencies (Node 18+ built-ins: http, fs, fetch)  |
|  - In-memory .env parser & prompt injection guardrails                  |
|  - Unified Git Diff Parser (reconstructs before/after file states)      |
|  - Anthropic Messages API Client (Claude 3.5 Sonnet)                   |
|  - Simulated SSE Streaming Engine for Demo Mode                         |
+--------------------+--------------------------------+-------------------+
                     |                                |
    POST api.anthropic.com/v1/messages    GET github.com/.../pull.diff
                     |                                |
            Anthropic Claude 3.5             GitHub Public API
```

### Core Architecture Principles:
1. **Zero External Dependencies**: Both server and frontend operate without `npm install`. The server uses native Node 18+ `http`, `fs`, and `fetch`.
2. **Client-Side Compute**: Line diffing and word-level diffing occur directly in the browser to avoid unnecessary roundtrips for editing actions.
3. **Prompt Injection Hardening**: All code inputs are encapsulated in rigid XML tags (`<version_a>` and `<version_b>`). The system prompt instructs the model to treat content strictly as passive data to analyze.
4. **Resilient JSON Recovery**: If Claude emits markdown fences or conversational text, the backend slices from the first `{` to the last `}` and normalizes missing fields to sensible defaults.
5. **Zero-Config Demo Mode**: When no `ANTHROPIC_API_KEY` is configured, the server defaults to Demo Mode with 3 pre-computed scenarios and a simulated chunked token stream.

---

## 4. Key Features & Algorithms

### 4.1. Intra-Line Word-Level Diffing
- **Algorithm**: Longest Common Subsequence (LCS) computed at the line level. Contiguous deletion and addition blocks are paired.
- **Tokenization**: Sub-token regular expression `/\w+|\s+|[^\w\s]+/g` isolates words, whitespace, and operators.
- **Visualization**:
  - Deleted words: `.diff-word-del` (red background, strikethrough).
  - Added words: `.diff-word-add` (green background, bold).

### 4.2. Code Syntax Highlighting Engine
- Embedded regex tokenizer handles JavaScript, TypeScript, and JSON keywords (`function`, `const`, `return`, `async`, `await`, etc.), strings, numbers, booleans, and comments without external CDN reliance.

### 4.3. Real-Time Server-Sent Events (SSE) Streaming
- When `stream: true` or `Accept: text/event-stream` is requested, `/api/analyze` establishes an SSE stream (`Content-Type: text/event-stream`).
- Emits:
  - `event: status` — connection status and active model.
  - `event: token` — incremental reasoning chunks.
  - `event: complete` — final parsed and validated JSON payload.

### 4.4. Automated SemVer Classification Heuristics
- Inspects model output and breaking change severity:
  - Any `High` severity breaking change $\rightarrow$ **Major Bump (v2.0.0)**
  - Any `Medium` or `Low` breaking change $\rightarrow$ **Minor Bump (v1.1.0)**
  - Zero breaking changes $\rightarrow$ **Patch Bump (v1.0.1)**

### 4.5. Direct GitHub PR & Commit Ingestion
- Accepts GitHub URLs:
  - Pull Requests: `https://github.com/:owner/:repo/pull/:number`
  - Commits: `https://github.com/:owner/:repo/commit/:sha`
  - Compares: `https://github.com/:owner/:repo/compare/:range`
- Fetches unified diffs with redirect handling.
- `parseUnifiedDiff` reconstructs original before and after states per file, rendering interactive file chips.

---

## 5. API Reference

### `GET /api/health`
Returns system status and demo mode indicator.
```json
{
  "ok": true,
  "demo": true
}
```

### `POST /api/analyze`
Analyzes code diffs.
- **Request Headers**: `Content-Type: application/json`, optional `Accept: text/event-stream`
- **Request Body**:
  ```json
  {
    "a": "function createUser(name, email) { ... }",
    "b": "function createUser({ name, email }) { ... }",
    "stream": true
  }
  ```
- **Response (`200 OK`)**:
  ```json
  {
    "demo": false,
    "semver_recommendation": "major",
    "summary": "createUser signature refactored to options object...",
    "architectural_impact": "Public contract altered, validation modularized...",
    "breaking_changes": [
      {
        "severity": "high",
        "title": "createUser signature changed",
        "detail": "Positional arguments will throw ValidationError..."
      }
    ],
    "release_notes_markdown": "## v2.0.0 (Major Release)\n\n### Breaking Changes..."
  }
  ```

### `POST /api/github`
Fetches and parses a public GitHub pull request or commit.
- **Request Body**: `{ "url": "https://github.com/facebook/react/pull/28000" }`
- **Response (`200 OK`)**:
  ```json
  {
    "title": "PR #28000 (facebook/react)",
    "type": "pull",
    "files": [
      {
        "filename": "packages/react-dom/client.js",
        "additions": 7,
        "deletions": 3,
        "before": "...",
        "after": "...",
        "patch": "..."
      }
    ]
  }
  ```

---

## 6. Spec-Driven Planning Artifacts

In accordance with the Devpost Build With AI Basics Hackathon guidelines, the project strictly maintained planning artifacts in the repository root before coding:
1. `scope.md`: Timebox constraints, in-scope requirements, out-of-scope boundaries, and risk mitigation strategies.
2. `prd.md`: Problem framing, target personas, functional priority matrix, and demo script.
3. `spec.md`: Architecture diagrams, prompt contracts, LCS line diff algorithms, and smoke test plans.

---

## 7. Running the Application

### Prerequisites
- Node.js 18 or higher.
- No `npm install` needed.

### Quick Start
```bash
# 1. Clone repository
git clone https://github.com/Nareshaspire/gittogether-diff.git
cd gittogether-diff

# 2. (Optional) Set API Key for live Claude analysis
cp .env.example .env
# Edit .env and set ANTHROPIC_API_KEY=your_key_here

# 3. Start server
node server.js
```
Open `http://localhost:3000` in any web browser.

---

## 8. Future Roadmap

1. **GitHub Action Integration**: Run GitTogether in CI/CD pipelines to automatically comment breaking change warnings on incoming PRs.
2. **Multi-File AST Analysis**: Deep syntax-tree resolution across entire repositories for cross-file symbol tracking.
3. **PR Webhook Bot**: Automated changelog syncing to Slack, Discord, and Linear.
