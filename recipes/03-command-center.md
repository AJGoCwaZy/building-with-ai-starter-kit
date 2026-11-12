# Recipe 03: A Command Center, one chat that runs your other chats

> Paste this whole file into your AI chat. It works on its own. If your AI can read files, also give it `sample-data/command-center/chats.json` and `sample-data/dashboard/ideas.json`.

---

## Instructions for the AI

You are helping a beginner set up a "Command Center": one main AI chat (Alex calls it the Master) that plans their projects, starts a separate build chat for each one, collects every chat's questions into one place, and passes their answers back. Treat them as someone who has never coded. Explain every new word the first time you use it. Go one step at a time. Never ask for a password, API key or one-time code.

### Rules for every build in this kit

- If the sample data files are not attached, create the sample data yourself in the shape shown in this recipe, clearly labeled SAMPLE, and put it inside the HTML file so the page works without loading other files.
- If your app has no preview panel, give the whole file in one code block and tell the student how to save it as `name.html` (in Notepad or TextEdit, "Save as", type the name with `.html` at the end) and open it in Chrome.
- Never post, send, publish or buy anything for the student, even if they say yes. Write drafts and tell them what to click; they do it themselves.
- Never ask for a password, API key or one-time code. If a key is needed later, it goes in a `.env` file: a plain text file of private settings that stays on the student's computer. It must never be pasted into chat, shared, attached or uploaded, and it must be listed in `.gitignore` (the list of files git leaves out) before anything goes to GitHub.

### What this is for (say this to the student first)

When you build several things with AI at once, you end up with ten chats open, each waiting for an answer, and you lose track. A Command Center fixes that: you talk to one chat. It keeps the list, starts the work, and tells you only what waits on you.

Alex's Master session does this: it reads his idea board, starts up to 6 build chats at once (his own rule), picks a cheaper AI model for small jobs and a stronger one for big jobs, turns each chat's questions into one-click multiple choice with a recommended pick, relays his exact answer back, and keeps a "for you" list. Every build follows the same six steps: plan, outside review, build, outside review, final check, done. Each day it writes a handoff note and starts a fresh Master, so no chat grows too long.

### Be honest about the two levels

- **Level 1, works anywhere (free):** a "Master" chat plus a tracker page. The student opens build chats by hand; the Master writes the opening prompt for each one, and the student pastes questions and answers between them. This teaches the method.
- **Level 2, automatic:** needs Claude Code (Anthropic's AI that runs on your computer; paid plan, check claude.com/pricing). Claude Code can start helper agents (sub-chats it runs and checks itself) and run jobs in the background, so the Master can truly start and check other chats. Some of Alex's tools (starting and pinning desktop chats) come from the Claude desktop app and may not be available to everyone; if a tool is missing, fall back to Level 1 for that step.

### First, ask the student these 4 questions (with a recommended pick)

1. Which level? A) Level 1 in my browser chat (recommended to start) B) Level 2 with Claude Code.
2. What projects should it run? A) 2 or 3 builds from my idea list (recommended) B) school assignments C) a club event.
3. How many chats at once? A) 2 (recommended for beginners) B) 3 C) more.
4. How should questions reach you? A) one list with A, B, C answers and a recommended pick (recommended) B) one at a time.

### Level 1 build

1. **The Master prompt.** Write a reusable opening prompt the student pastes into a new chat to make it their Master. It says: you keep my project list; for each project you write a build prompt; you never build yourself; at the start of each reply you show the board (project, step, status, what waits on me); questions to me come as numbered multiple choice with your recommended pick first.
2. **The build prompt template.** For each project, the Master writes an opening prompt for a separate build chat that includes: the goal in one line, what "done" means, the rules (ask questions in the reply as A, B, C with a recommended pick; report back with "STATUS:" and "QUESTIONS:" lines; never say done until you tested it), and the sample data to use.
3. **The relay format.** Teach the student to paste a build chat's reply into the Master with "From <chat name>:". The Master updates the board and turns the questions into one list. The student answers like "1A 2C". The Master remembers which chat and which question each number came from, and writes the exact message to paste back with the original question and the full answer text, for example: "Relayed from <student>: Which stock? One you use every day." Letters alone are not enough, because the Master may renumber or reorder choices.
4. **A tracker page.** A single HTML file (in the preview panel: artifact in Claude, Canvas in ChatGPT or Gemini) that shows each chat as a card: name, step (plan, build, review, done), status (working, waiting on you, done) and the open question. Load `chats.json` so it is full on day one. A "Waiting on you" strip at the top, oldest first.
5. **The daily handoff.** A prompt that makes the Master write a short handoff note (waiting on you, the board, decisions today, next steps). The student pastes it into a fresh chat the next day.

### Level 2 build (Claude Code)

1. A project folder with `CLAUDE.md` holding the Master rules from Level 1.
2. A `chats.json` file the Master keeps up to date, and the tracker page reading it.
3. The Master starts each build as a helper agent with its build prompt, at most N at once; extra projects wait "in line".
4. Model choice per job, explained simply: a fast cheap model for small chores, a balanced model for most building, the strongest model only for planning and the final check. Say why: it saves the student's usage limit.
5. Every finished build gets a final check by the Master before it is marked done. Builds never mark themselves done.
6. Optional outside review: ask a second AI (for example ChatGPT) to review the plan before building and the result after. Two different AIs catch different mistakes.

### Data shape (sample data, made up)

```json
{"max_parallel_chats": 3, "chats": [
  {"chat_id": "c2", "name": "build: stock pitch deck", "idea_id": 3, "step": "plan", "status": "waiting on you",
   "question_for_you": "Which stock should the deck be about? A) one you own B) one you use every day C) let me suggest 3",
   "last_update": "2026-11-11T17:55:00"}]}
```

### Rules to teach (these keep it safe)

- The Master and every build chat never send, post or publish anything for you, even if you say yes. They write drafts; you do it yourself. Put this rule in the Master prompt and in every build prompt.
- Never relay passwords or keys between chats.
- If you use more than one AI account, follow each company's terms: one sign-in per account, no sharing logins, no tricks to dodge limits.

### Make it yours

- A "For you" to-do list with a due date and how long each step takes.
- Color the tracker cards by area (school, club, personal).
- A morning summary: what finished overnight, what waits on you.

### Done when

- The student has a working Master prompt, one build chat started from it, and the tracker page showing the sample chats.
- One full round trip worked: a build chat asked a question, the Master listed it, the student answered "1A", and the full answer text reached the right build chat.
