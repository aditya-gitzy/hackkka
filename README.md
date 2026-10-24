# DevSight AI

DevSight is a local-first, full-stack workspace for inspecting a running web app, understanding browser findings, reviewing a source change, and rerunning the app to verify the result. It includes beginner and Pro themes. The supplied navy design stylesheet is preserved in `static/workspace-original.css`; workspace additions live in separate files.

## Start on Windows

Open two PowerShell terminals in this folder.

**Terminal 1 — DevSight UI and API** (run `.\setup.ps1` once if the Python environment is not set up):

```powershell
.\.venv311\Scripts\python.exe -m uvicorn main:app --host 127.0.0.1 --port 8000
```

**Terminal 2 — sample Next.js app** (run `npm install` once in `sample-next`):

```powershell
cd sample-next
npm run dev
```

Open [http://127.0.0.1:8000](http://127.0.0.1:8000). DevSight selects the sample project and `/events` route by default. Click **Run audit**, select a finding, inspect its evidence and source, then generate or edit a small replacement. **Apply fix** writes the edit after making a backup and reloads the local route; a clean rerun verifies it. **Undo** restores the original snippet. The sample starts with three seeded runtime errors.

To inspect another app, enter its absolute project folder and its `http://localhost` or `http://127.0.0.1` development URL. DevSight only connects to loopback hosts. Findings, project source and screenshots remain local unless you enable model analysis.

## Gamification

- Diagnose a finding from evidence before seeing the cause; ask for up to five progressively clearer hints or reveal the solution at any time.
- Earn XP for scans, new evidence, a correct diagnosis, a verified fix, independent solving, and the post-fix learning question.
- Progress through Apprentice, Investigator, Debugger, Engineer, and Mentor levels; unlock evidence, diagnosis, independent-solver, and fix badges.
- Seeded sample findings are labeled as practice; live localhost findings are labeled separately.
- Beginner and Pro themes, animated audit steps, and reduced-motion support.

Progress is saved in this browser's local storage. XP for fixes is awarded only after the verification rerun finds neither the selected issue nor new browser findings.

## Gemma analysis

The app uses rule-based browser observations without a model key. To enable Gemma, add `GEMINI_API_KEY=...` to the ignored local `.env` file and set `GEMINI_MODEL=gemma-4-26b-a4b-it`. Do not paste keys into chat or commit them. Rotate any key that has been exposed.

Gemma receives the captured local browser evidence and selected project source when analysis is enabled. Review every model suggestion. The Apply action checks that the target text still matches exactly once and creates a backup in `.devsight/backups/` before writing. Do not use this local single-user development service on a public network.
