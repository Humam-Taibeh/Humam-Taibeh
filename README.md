## 🚀 Featured Projects

### 🔔 [UniNotifier](https://github.com/Humam-Taibeh/UniNotifier)
**My university, on my phone, the moment anything changes.** A Windows background service that watches my university's Moodle and sends everything that matters to a private Telegram bot of my own. No server, no subscription; nothing leaves the PC except the messages sent to my bot.

* **Course monitoring:** new files, assignments, quizzes, announcements, forum posts and Teams lectures, each sent as a screenshot of the item or the file itself. Edits show what changed (*Was* / *Now*).
* **Automatic archive:** every file is saved per course into `01_Lectures` / `02_Assignments` / `03_Exams`, never twice. A new version from the instructor replaces the old one, which moves to `_Old_Versions`.
* **Deadlines & lectures:** reminders 24 h and 1 h before assignments and quizzes, a daily list of open tasks, and lecture alerts with a **Join** button. Automatic attendance check-in is optional.
* **Marks & GPA:** detects released marks, finds my row inside marks files (Excel, Word, PDF) by student ID, and includes a "grade needed" calculator and a GPA planner.
* **Degree tools:** transcript and balance on demand, degree progress from my own study plan, and a **Registration Plan** that suggests what to register next term from prerequisites and credit-hour rules.
* **Self-managing:** the bot restarts itself, relays Microsoft 2FA to Telegram, detects maintenance, and offers one-tap updates that roll back if the new version doesn't start.

<details>
<summary><b>Under the hood</b></summary>

* **Two Windows scheduled tasks:** `monitor.py` runs a check every 15 minutes (plain HTTP with a saved session; headless Chromium only for sign-in and screenshots). `bot.py` is always on, answers commands and takes a tiny look at Moodle every 2 minutes.
* **Diff-based tracking:** each scan is compared with the previous saved state, so only real changes are announced. The first run records a baseline and stays quiet.
* **Stale-while-revalidate** for the registration portal: answers instantly from the last copy and refreshes in the background.
* **Privacy & security:** credentials live in a git-ignored `.env` and are masked in logs and error alerts; the bot serves a single owner; a test fails if any personal file is ever tracked by Git.
* **Quality:** an offline test suite (any outside network call fails the run), pyflakes-clean code, GitHub Actions CI, a built-in `doctor` diagnostic tool, an installer, and documentation in English and Arabic.
</details>

**Stack:** Python · Playwright · Telegram Bot API · Windows Task Scheduler · PowerShell

---

### 🏛️ [Pulse](https://github.com/Humam-Taibeh/Pulse)
Windows deployment & optimization toolkit: a modular PowerShell core with a PySide6 (Qt 6) desktop interface and asynchronous task execution.

**Stack:** PowerShell 5.1 · Python · PySide6

---

### 🌿 [GreenDrive](https://github.com/Humam-Taibeh/GreenDrive)
Route optimization app built for a Google hackathon (participation certificate). Factors Amman's terrain elevation into fuel and emissions estimates, with Gemini-generated insights.

**Stack:** React · Vite · Gemini API · Google Cloud

---

### 🚀 [Rise](https://github.com/Humam-Taibeh/Rise)
Task and workflow manager with real-time CRUD state on a Supabase backend.

**Stack:** React · Vite · Supabase (PostgreSQL)

---

### 📚 DevCore 🔒 *(private repository)*
**A self-paced Backend & AI Engineering program in Arabic (Jordanian dialect, RTL).** It turns a long roadmap into 4 sections → 21 modules → week-sized sub-sections → one task at a time, so the learner always knows the single next thing to do. About 1,050 hours of content, with progress in percent and no deadlines.

* **One task at a time:** a "Today" view with the single next task, and a study player that shows one step with its new terms and a ready template (README, ADR, design doc) when needed.
* **Exams built from what you studied:** weekly, module, terms, phase and final exams; a module exam unlocks at 80% completion. A placement test (85% to pass) lets learners skip modules they already know.
* **Study partner:** a small progress summary shared only with a partner who accepted the request.
* **Local-first, installable PWA:** progress saves in the browser first, so the app is instant and works offline.
* **Cloud sync:** when signed in, progress syncs across devices in real time and merges safely when two devices change things at once. No finished step is ever lost.

<details>
<summary><b>Under the hood</b></summary>

* **Sync engine:** an optimistic-concurrency write (`save_progress` RPC) that only replaces the stored state if the client's base version is still current. On conflict it fetches the cloud copy, merges (union of finished steps and study days, best exam score kept) and retries. Realtime updates come from Supabase.
* **Planner:** splits each month's core hours into balanced weeks (dynamic programming plus local repair); the plan has no calendar dates.
* **Security:** row-level security on every table; accounts need admin approval (invites skip it); changes to memberships and partnerships go only through checked database functions; the build refuses to run if a Supabase secret key is placed in a `VITE_*` variable; strict CSP, HSTS and `X-Frame-Options` headers.
* **Testing:** Vitest unit tests (content integrity, state, planner, sync engine, and the SQL schema on a real Postgres via PGlite) plus Playwright end-to-end tests on desktop and mobile; ESLint and Prettier.
</details>

**Stack:** Vanilla JS · Vite · Supabase (Postgres, RLS) · Vitest · Playwright
