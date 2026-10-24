# GitTogether — Visual Diff & Breaking Change Intelligence (PoC)

> Built for the **Devpost: Build With AI Basics Hackathon** using AI planning skills (`scope.md`, `prd.md`, `spec.md`).

**GitTogether** transforms raw git diffs and code snippets into actionable architectural intelligence. In seconds, it generates:
1. **Interactive Visual Line Diff**: Full unified diff with line numbers, addition/deletion indicators, and diff stats.
2. **SemVer Version Bump Recommendation**: Intelligent classification (`Major`, `Minor`, or `Patch`) based on breaking change severity.
3. **Plain-English Executive Summary**: High-level overview of what changed.
4. **Architectural Impact & Blast Radius**: How module boundaries, data flow, dependencies, and performance are affected.
5. **Breaking Change Flags**: Categorized with severity badges (`High`, `Medium`, `Low`) and specific affected callers.
6. **Instant Markdown Release Notes**: Formatted for GitHub Releases / changelogs with one-click copy and file download.

---

## Quickstart

### Prerequisites
- Node.js 18+
- Zero dependencies required (`npm install` is not needed!)

### Run the App
```bash
# 1. (Optional) Configure live Claude API key
cp .env.example .env
# Edit .env and set ANTHROPIC_API_KEY=your-key-here

# 2. Launch the server
node server.js
```

Open **`http://localhost:3000`** in your browser.

> **Zero-Config Demo Mode**: If no API key is set, GitTogether automatically runs in Demo Mode with three pre-configured real-world scenarios so anyone can test and record the complete workflow instantly without an account.

---

## Built-In Scenarios

- 🚀 **Scenario 1: API Refactor (Breaking)** — Changes `createUser` from positional args to an options object, throwing `ValidationError`. Surfaces a **Major Bump (v2.0.0)** with high-severity breaking flags.
- ⚡ **Scenario 2: Redis Cache Layer (Non-Breaking)** — Introduces in-memory caching to `getUserProfile`. Surfaces a **Minor Bump (v1.1.0)** with zero breaking changes.
- 🛡️ **Scenario 3: Security Sanitization (Patch)** — Adds DOMPurify XSS protection to `renderMarkdown`. Surfaces a **Patch Bump (v1.0.1)** bug fix.

---

## Planning Documents

In accordance with the Devpost Build With AI Basics specification:
- [scope.md](scope.md) — Kernel definition, in-scope requirements, out-of-scope boundaries, and risk mitigations.
- [prd.md](prd.md) — Problem statement, user stories, functional requirements, demo script, and success criteria.
- [spec.md](spec.md) — Technical architecture, API contracts, prompt design, line diff algorithm, and smoke tests.

---

## Demo Script (under 2 minutes)

1. **(0:00 - 0:20)** State the problem: Code reviews and changelog writing take time, and subtle breaking changes get missed under pressure.
2. **(0:20 - 0:45)** Open `http://localhost:3000`, select **Scenario 1**, and point out the side-by-side inputs and visual diff.
3. **(0:45 - 1:15)** Click **Analyze Changes**. Walk through the **Major Bump (v2.0.0)** badge, the Plain-English Summary, and the flagged Breaking Change (`createUser` signature change).
4. **(1:15 - 1:40)** Click **Copy Markdown** on the release notes block and show the toast confirmation. Switch to **Scenario 2** to demonstrate a non-breaking **Minor Bump**.
5. **(1:40 - 2:00)** Conclude: Built using spec-driven development with AI planning skills. Next steps: GitHub Action integration and PR webhook bots.

---

## License
MIT
