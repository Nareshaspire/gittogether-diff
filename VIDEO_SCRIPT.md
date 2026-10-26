# GitTogether — Official Hackathon Video Demo Script

**Hackathon:** Devpost: Build With AI Basics  
**Target Duration:** 1:30 – 2:30 minutes (Strictly within the 1 to 3 minute limit)  
**App URL:** `http://localhost:3000`  
**Repository:** [https://github.com/Nareshaspire/gittogether-diff](https://github.com/Nareshaspire/gittogether-diff)  

---

## 🎯 Pre-Recording Checklist
- [ ] Terminal open and running `node server.js`
- [ ] Browser open at `http://localhost:3000` (set zoom to 110%)
- [ ] GitHub repository tab open at `https://github.com/Nareshaspire/gittogether-diff`
- [ ] Screen recording tool ready (Loom, OBS, or system recorder)

---

## 🎬 Timestamped Script & Screen Directions

### ⏱️ Act 1: The Problem & The Solution (0:00 – 0:25)
**Action on Screen:**
- Start on `http://localhost:3000`. Show the sleek dark-mode dashboard, header, and editor panes.

**Voiceover Script:**
> *"Hi everyone, this is **GitTogether** — an AI-powered code diff intelligence tool built for the **Devpost: Build With AI Basics Hackathon**.*
>
> *Reviewing pull requests is mentally exhausting. Under deadline pressure, subtle breaking changes easily slip into production, understanding the full architectural blast radius takes too long, and writing release notes by hand is tedious. GitTogether solves all three in seconds."*

---

### ⏱️ Act 2: Enhanced Visual Diff & Intra-Line Highlighting (0:25 – 0:50)
**Action on Screen:**
- Click **Scenario 1: API Refactor (Breaking)** on the toolbar.
- Scroll down slightly to the **Enhanced Visual Diff**.
- Toggle the **Word-level Diff** checkbox off and back on.

**Voiceover Script:**
> *"Here we have Scenario 1: an API refactor. Instead of a plain line diff that just highlights full lines, GitTogether features **intra-line word-level diffing** and syntax highlighting.*
>
> *Notice how it precisely pinpoints the exact modified tokens: the old positional arguments `name, email` are struck through in red, and the new options object `{ name, email, role = 'member' }` is highlighted in vibrant green."*

---

### ⏱️ Act 3: Real-Time SSE Streaming & SemVer Intelligence (0:50 – 1:20)
**Action on Screen:**
- Click **Analyze Changes**.
- Show the **Live AI Streaming Inspector** terminal with the glowing pulse ring as tokens stream in.
- Watch the stream finish, revealing the **SemVer Major Bump** banner.
- Scroll down to show the **Executive Summary**, **Architectural Impact**, **Breaking Changes**, and **Release Notes**.
- Click **Copy Markdown** and **Download .md** (point out the toast).

**Voiceover Script:**
> *"When I click **Analyze Changes**, our Server-Sent Events engine streams the AI analysis in real time directly into this interactive terminal inspector.*
>
> *As soon as it completes, GitTogether automatically recommends a **SemVer Major Bump (v2.0.0)** because breaking changes were detected. Below, it provides a plain-English executive summary, traces the architectural blast radius, and flags breaking changes with severity badges—explaining that callers must update to the options object signature.*
>
> *At the bottom, it generates publish-ready markdown release notes that you can copy or download in one click."*

---

### ⏱️ Act 4: Direct GitHub PR Ingestion & Wrap-Up (1:20 – 1:45)
**Action on Screen:**
- Scroll back to the top to the **GitHub Ingestion Bar**.
- Click **Try Sample PR**. Show the PR banner and file selector chips.
- Click a file chip.
- Switch to the GitHub repository tab showing `scope.md`, `prd.md`, and `spec.md`.

**Voiceover Script:**
> *"GitTogether also connects directly to GitHub. By pasting any public PR or commit URL — or clicking 'Try Sample PR' — it ingests the unified diff, displays the PR title, and renders interactive file selector chips so you can review multi-file PRs instantly.*
>
> *Under the hood, GitTogether has **zero npm dependencies**, runs on native Node.js, and was built following spec-driven AI development with `scope.md`, `prd.md`, and `spec.md` preserved in the repo.*
>
> *Thank you for watching!"*

---

## 💡 Scoring Alignment Notes for Judges
- **Design Score**: Highlight the responsive dark mode, intra-line word diff contrast, and glowing status indicators.
- **Innovation Score**: Emphasize real-time SSE streaming terminal and automated SemVer classification.
- **Presentation Score**: Clear problem-solution flow, demonstrated live end-to-end, under 2 minutes.
