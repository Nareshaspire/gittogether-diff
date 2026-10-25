# GitTogether — Visual Diff & Breaking Change Intelligence (PoC)

> Built for the **Devpost: Build With AI Basics Hackathon** using AI planning skills (`scope.md`, `prd.md`, `spec.md`).

**GitTogether** transforms raw git diffs, GitHub PRs, and code snippets into actionable architectural intelligence. In seconds, it generates:
1. **Interactive Visual Line Diff**: Full unified diff with line numbers, addition/deletion indicators, and diff stats.
2. **Intra-Line Word-Level Diffing & Syntax Highlighting**: Highlights exact character/word changes within modified lines, with toggles for word diffing and language syntax highlighting.
3. **Direct GitHub PR & Commit Fetching**: Ingest diffs directly from any public GitHub PR or commit URL (`https://github.com/:owner/:repo/pull/:number`) with multi-file chip selection.
4. **Real-time Server-Sent Events (SSE) Streaming**: Live chunk-by-chunk streaming inspector for Claude 3.5 Sonnet and Demo Mode.
5. **SemVer Version Bump Recommendation**: Intelligent classification (`Major`, `Minor`, or `Patch`) based on breaking change severity.
6. **Plain-English Executive Summary**: High-level overview of what changed.
7. **Architectural Impact & Blast Radius**: How module boundaries, data flow, dependencies, and performance are affected.
8. **Breaking Change Flags**: Categorized with severity badges (`High`, `Medium`, `Low`) and specific affected callers.
9. **Instant Markdown Release Notes**: Formatted for GitHub Releases / changelogs with one-click copy and file download.

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

## License
MIT
