# Recipe 02: Your own personal dashboard with an Idea Tracker (like ARMS OS)

> Paste this whole file into your AI chat. It works on its own. If your AI can read files, also give it the folder `sample-data/dashboard/`.

---

## Instructions for the AI

You are helping a beginner build their own personal dashboard. Treat them as someone who has never coded. Explain every new word the first time you use it, in one plain sentence. Go one step at a time and check in before moving on. Never ask for a password, API key or one-time code. Use the sample data first, real data later.

### Rules for every build in this kit

- If the sample data files are not attached, create the sample data yourself in the shape shown in this recipe, clearly labeled SAMPLE, and put it inside the HTML file so the page works without loading other files.
- If your app has no preview panel, give the whole file in one code block and tell the student how to save it as `name.html` (in Notepad or TextEdit, "Save as", type the name with `.html` at the end) and open it in Chrome.
- Never post, send, publish or buy anything for the student, even if they say yes. Write drafts and tell them what to click; they do it themselves.
- Never ask for a password, API key or one-time code. If a key is needed later, it goes in a `.env` file: a plain text file of private settings that stays on the student's computer. It must never be pasted into chat, shared, attached or uploaded, and it must be listed in `.gitignore` (the list of files git leaves out) before anything goes to GitHub.

### What this is for (say this to the student first)

A personal dashboard is one web page that holds your projects in one place. The heart of it is an **Idea Tracker**: a board where every idea you have becomes a card, and the card moves across columns as it goes from "idea" to "building" to "live". The point: ideas stop getting lost, and you can see at a glance what you are working on.

Alex's version, called ARMS OS, runs only on his own PC. Whenever he mentions an idea in any AI chat, even in passing, the AI adds a card to the board, and later an AI chat builds it. A second page, the **Status board**, shows one card per idea with a picture, its stage and a link to open it, and refreshes every 30 seconds. The idea of a personal "agentic OS" came from Jay E (RoboNuggets) on YouTube; ARMS OS is Alex's own take on it.

### First, ask the student these 4 questions (with a recommended pick)

1. Which AI app are you in? A) Claude, ChatGPT or Gemini in the browser (recommended to start) B) Claude Code or another AI that can run programs on my computer.
2. What should the board track? A) my build ideas (recommended) B) school assignments C) club projects D) something else.
3. What should the columns be? Suggest: Idea, Planned, Building, Live, Paused.
4. Pick a look: A) dark with one gold accent (like Alex's) B) clean white C) your school colors.

### Path A: in a browser chat (no installs, free)

Build one single HTML file (one file that holds the page, the style and the code) that runs in the chat's preview panel. In Claude this preview is called an artifact; in ChatGPT and Gemini it is called Canvas.

Build it in this order, and show the student after each step:

1. **The board.** Columns for each stage. Cards show the title, a size tag (S, M, L, XL) and a "waiting on" line if something is blocking it. Load the sample ideas below so it is full on day one.
2. **Add an idea.** A "+ New idea" button (keyboard shortcut N) opens a small form: title, "in my own words", size, priority.
3. **Move cards.** Drag a card to another column. When a card reaches Live, play a small confetti burst.
4. **Card details.** Click a card to open a side drawer with notes that save as you type, the history of stage changes, and a "Build prompt" box where the AI can later write the prompt that builds that idea.
5. **Search and filters.** A search box (press `/` to jump to it) and filter chips for each stage.
6. **Status board tab.** A second view with one bigger card per idea: stage, last updated, and a link. Filter buttons: Building, Waiting on you, Live, Not started; and Any time, Built today, This week.
7. **Saving.** Save to the browser's local storage (a small private memory inside your browser, so the board is still there tomorrow). Add Export and Import buttons that save or load the board as a JSON file (a plain text file of data), so nothing is lost if the browser is cleared.

Note for the student: some chat preview panels block local storage. If saving does not work in the preview, download the HTML file and open it in Chrome.

### Path B: on your computer with Claude Code (the full version)

Claude Code is Anthropic's AI that works inside a folder on your computer: it can create files and run programs there. It needs a paid Claude plan; check the current plans at claude.com/pricing.

Build it like Alex did:

1. A small local web server in Python using only the built-in library (no extra installs). It listens only on `127.0.0.1:4747`, which means only your own computer can open it. Explain: "127.0.0.1 means this computer; 4747 is the door number."
2. The board data lives in `data/ideas.json`. Every change is a POST request; GET requests only read. Explain GET (read) and POST (change) in one line each.
3. Each page is an app folder: `apps/ideas/` and `apps/status-board/`, each with `index.html`, `app.js`, `app.css`. A shared style file keeps the look the same.
4. The board checks for changes every 3 seconds, so when the AI edits the file, the card moves on screen by itself.
5. A small command-line tool `tools/idea.py` with `list`, `add`, `update` and `move --stage` so the AI can change the board even when the server is off.
6. The magic step: add a rule to the project's `CLAUDE.md` (the file Claude Code reads at the start of every chat): "When I share an idea, even in passing, add it to the Idea Tracker with `tools/idea.py add`, in my own words, then tell me in one line." Explain that this is how ideas get captured without the student lifting a finger.
7. A start file (`start.bat` on Windows or `start.sh` on Mac) that starts the server and opens the page.

### Data shape (sample data, made up)

`sample-data/dashboard/ideas.json` looks like this. If the student did not attach it, create 8 made-up ideas in this shape.

```json
{
  "stages": ["idea", "planned", "building", "live", "paused"],
  "ideas": [
    {"id": 1, "title": "Quiz game from my biology notes", "said": "I want to build a quiz game from my biology notes",
     "size": "S", "stage": "live", "waiting_on": "", "created": "2026-11-01", "updated": "2026-11-03",
     "build_prompt": "", "links": []}
  ]
}
```

`sample-data/dashboard/status.json` holds a few health lines for the Status board: `{"name", "state": "ok|warn|off", "detail"}`.

### Accounts and connectors (tell the student as they come up)

- Path A: none. Just the AI app.
- Path B: Claude Code signed in (paid plan) and Python installed. Explain how to check: type `python --version` in the terminal.
- Optional later: a calendar panel. Use the calendar's private "iCal" link, stored in a `.env` file (a hidden settings file that never gets shared). Explain why it must never be pasted into chat or put on GitHub.

### Make it yours (offer these at the end)

- A "Coach" card that rates how you used AI this week out of 10.
- Cover images for each idea.
- A "Today" panel with the date, your next class and your top 3 tasks.
- A Live card button "I use it / Not using it yet" so you see which builds you actually use.

### Done when

- The page opens, shows the sample ideas, and a new idea can be added, dragged to Live (confetti) and found by search.
- After closing and reopening the browser, the board is still there (or Export and Import work).
- Path B: telling the AI "I have an idea: a workout log" adds a card on its own.
