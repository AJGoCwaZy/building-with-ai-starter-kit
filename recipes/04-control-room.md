# Recipe 04: A Control Room, your AI usage and model dashboard

> Paste this whole file into your AI chat. It works on its own. If your AI can read files, also give it `sample-data/control-room/usage.json` and `sample-data/control-room/transcript-sample.jsonl`.

---

## Instructions for the AI

You are helping a beginner build a Control Room: one page that shows which AI chats are working, which are waiting on them, which model each one uses, how much each one used, and how close they are to their plan's limits. Treat them as someone who has never coded. Explain every new word the first time you use it. Go one step at a time. Never ask for a password, API key or one-time code.

### Rules for every build in this kit

- If the sample data files are not attached, create the sample data yourself in the shape shown in this recipe, clearly labeled SAMPLE, and put it inside the HTML file so the page works without loading other files.
- If your app has no preview panel, give the whole file in one code block and tell the student how to save it as `name.html` (in Notepad or TextEdit, "Save as", type the name with `.html` at the end) and open it in Chrome.
- Never post, send, publish or buy anything for the student, even if they say yes. Write drafts and tell them what to click; they do it themselves.
- Never ask for a password, API key or one-time code. If a key is needed later, it goes in a `.env` file: a plain text file of private settings that stays on the student's computer. It must never be pasted into chat, shared, attached or uploaded, and it must be listed in `.gitignore` (the list of files git leaves out) before anything goes to GitHub.

### What this is for (say this to the student first)

AI plans have usage limits (for Claude, a 5-hour window and a weekly limit). When you run several chats, it is easy to burn through your limit on the wrong thing. The Control Room is a speedometer: one glance shows what is running, what it costs, and how much room is left.

Alex's Control Room runs only on his PC at `127.0.0.1:4317` (127.0.0.1 means "this computer"; 4317 is the door number). Every 5 seconds it reads the log files Claude Code already writes, and it uses no AI at all to do that, so it costs nothing to run. It shows: two gauges for the 5-hour and weekly limits (gold when getting high), "Running now" cards with a "needs you" tag, a lineup of the models working (shown as little pixel characters), a cost card that compares what he used against what it would have cost if everything ran on the most expensive model, and a history table. The history never shows message text, only numbers.

### Be honest about what it needs

- The full live version reads the log files of **Claude Code** (Anthropic's AI that runs on your computer; paid plan, check claude.com/pricing). Claude Code saves each chat as a `.jsonl` file (one line of data per message) in the `.claude/projects` folder in your home folder.
- Students without Claude Code build the same dashboard on the **sample data**. It looks and works the same; it just shows made-up chats.

### First, ask the student these 3 questions (with a recommended pick)

1. Which version? A) sample data in my browser chat (recommended to start) B) live, reading my own Claude Code logs.
2. Main thing to see? A) what is running and waiting on me (recommended) B) how much I used today C) both.
3. Look? A) dark control room with one gold accent and pixel characters (like Alex's) B) clean white C) your own colors.

### Version A: sample data in the browser (free)

Build one single HTML file in the preview panel (Claude: artifact; ChatGPT and Gemini: Canvas) that loads the sample `usage.json` and shows:

1. **Two gauges:** 5-hour used and weekly used, per plan. Turn gold above 70 percent of the 5-hour window and above 80 percent of the weekly limit.
2. **Running now:** a card per chat with the title, project, model, status, and a "needs you" tag when status is "waiting on you".
3. **Model lineup:** one small pixel-art character per model family (draw them in CSS or SVG, do not copy anyone's logo or mascot), animated when that model is working.
4. **Usage table:** tokens in and out per chat, sortable. Explain: a token is a small piece of a word; AI usage is counted in tokens.
5. **A cost card (optional):** what the usage would cost at public API prices. Prices change: put them in one `prices` object with an "as of" date, and if you do not know today's prices, mark them `[CHECK]` and ask the student to look them up on the company's pricing page.
6. **An advice box:** "Good time for a big job" or "Wait, you are near your limit", based on the gauges.

### Version B: live, on your computer (Claude Code)

1. A tiny local server (Node.js or Python, built-in libraries only) that listens only on `127.0.0.1` and refuses requests from other computers.
2. Every 5 seconds it reads the Claude Code `.jsonl` files from the student's `.claude/projects` folder. From each assistant line it takes only: the time, the session id, the model name and the `usage` numbers (input, output, cache reads). The same reply can appear on several lines, so count each reply once. Never read or show the message text.
3. Status is a guess from the logs, so label it honestly: "working" if the chat wrote to its log in the last 30 seconds, "likely waiting on you" if its last entry is a reply from the AI with no tool still running, "idle" after 10 minutes of quiet, and "unknown" when you cannot tell.
4. A `/api/snapshot` route that returns a summary in the same shape as `usage.json`, and the page from Version A reading it.
5. Limits: Claude Code can run a status line script (a line at the bottom of the terminal) and hands it information about the session. First check the current Claude Code status line documentation for which fields it sends; if it includes 5-hour and weekly limit use, save those to a file the server reads. If it does not, show the gauges as "unknown" with a box where the student can type the numbers from their usage page. Explain that the script is a change to their Claude Code settings and ask before making it.
6. If reading a file fails, keep showing the last good numbers with a small warning banner, never a blank page.
7. A start file (`start.bat` or `start.sh`) that runs the server and opens the page.

### Data shapes (sample data, made up)

`usage.json`:

```json
{"generated": "2026-11-11T18:00:00",
 "plans": [{"name": "Plan A (sample)", "five_hour_used_pct": 42, "weekly_used_pct": 31, "resets_at": "2026-11-11T21:00:00"}],
 "sessions": [{"session_id": "s-001", "project": "quiz-game", "title": "Sample chat 1", "model": "sonnet",
   "status": "working", "started": "2026-11-11T08:05:00", "last_active": "2026-11-11T09:40:00",
   "input_tokens": 120000, "output_tokens": 9000, "tool_calls": 40}]}
```

`transcript-sample.jsonl` shows three made-up lines in the shape of a Claude Code log (type, timestamp, sessionId, message.model, message.usage).

### Privacy rule

Logs can hold private chats. The dashboard reads numbers only, never message text, and never sends anything off the computer.

### Make it yours

- A history view: one row per day with tokens per model.
- A "which model should I use" tip card.
- A small always-on-top mini view.

### Done when

- The page opens and shows gauges, running cards with "needs you" tags, and the usage table from the sample data.
- Version B: starting a new Claude Code chat makes a new card appear within 5 seconds.
