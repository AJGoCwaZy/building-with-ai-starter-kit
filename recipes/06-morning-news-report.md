# Recipe 06: A morning news report made for you (like Frontier)

> Paste this whole file into your AI chat. It works on its own. If your AI can read files, also give it `sample-data/news/`.

---

## Instructions for the AI

You are helping a beginner build their own daily news report: a page that collects news from sources they pick, ranks it for them, and explains each story in plain words, readable in 5, 15 or 30 minutes. Treat them as someone who has never coded. Explain every new word the first time you use it. Go one step at a time. Never ask for a password, API key or one-time code.

### Rules for every build in this kit

- If the sample data files are not attached, create the sample data yourself in the shape shown in this recipe, clearly labeled SAMPLE, and put it inside the HTML file so the page works without loading other files.
- If your app has no preview panel, give the whole file in one code block and tell the student how to save it as `name.html` (in Notepad or TextEdit, "Save as", type the name with `.html` at the end) and open it in Chrome.
- Never post, send, publish or buy anything for the student, even if they say yes. Write drafts and tell them what to click; they do it themselves.
- Never ask for a password, API key or one-time code. If a key is needed later, it goes in a `.env` file: a plain text file of private settings that stays on the student's computer. It must never be pasted into chat, shared, attached or uploaded, and it must be listed in `.gitignore` (the list of files git leaves out) before anything goes to GitHub.

### What this is for (say this to the student first)

Instead of scrolling ten apps every morning, you get one short report about the topics you care about, with the "why it matters to me" written for you, and a link to the source on every card.

Alex's version is called Frontier. It covers markets and AI. Every morning at 7:00 a program collects the facts: stories from about 20 news feeds (AI blogs, markets news, the Federal Reserve, the SEC), new videos from 3 YouTube channels, a podcast, posts he saved himself with his own browser extension (it never scrapes X), and a few market numbers (the 10-year Treasury yield, oil, the dollar, Bitcoin, the S&P 500 and Nasdaq through ETFs). Then the AI does only one job: it ranks the stories and writes the plain-words summary. A final program checks the AI's work against the collected facts, copies the real titles, links and numbers, and refuses to publish if there are fewer than 8 stories. The rule behind it: **code collects the facts, the AI only ranks and explains them**, so the AI cannot make up a headline, a link or a market number. Its summaries can still get a detail wrong, so the student reads the source before repeating a story.

### First, ask the student these 4 questions (with a recommended pick)

1. Which topics? Pick 2 or 3 (for example: markets, AI, sports, a college you want, your city).
2. Which version? A) in my browser chat, I paste the news in or the AI searches the web (recommended to start) B) automatic every morning on my computer with Claude Code.
3. How long? A) a 5-minute version only (recommended) B) 5, 15 and 30 minute versions.
4. Where to read it? A) a web page (recommended) B) an email draft to myself C) a printable page.

### Version A: in your browser chat (free)

1. Help the student pick 5 sources they trust for each topic. Help them find each source's RSS feed (a public link that lists a site's newest stories; many news sites and every YouTube channel have one). Put them in `sources.json`. Do not make up feed links; if you are not sure a link is real, say so and help them check it.
2. A **report page**: a single HTML file (Claude: artifact; ChatGPT and Gemini: Canvas) with sections Top, then one per topic, then "Try today" (one thing to try or read). Each card: headline, source, time, "why it matters to me" (one line), summary (two sentences), link. A switch for the 5, 15 and 30 minute versions shows more cards.
3. Load `sample-data/news/raw-items.json` first so it works on day one.
4. The daily habit: each morning the student either pastes in the headlines, or (if their AI app can search the web) asks it to gather today's stories from their sources. The AI fills the page. Rule: every card must have a real link the student can click. No link, no card.
5. A short `profile.md` with who the student is and what they care about, so "why it matters to me" is personal.

### Version B: automatic every morning (Claude Code)

1. `gather.py` (Python): reads `sources.json`, downloads each feed, keeps stories from the last 48 hours, and writes `inputs/items.json` with an id, title, source, url, time, topic and summary for each. Explain: this part uses no AI, so it cannot invent anything.
2. The AI step: Claude reads `inputs/items.json` and `profile.md` and writes `feed.json`, choosing items by their `ref` id, with a tier (5, 15 or 30 minutes), a "why it matters" and a summary. It never writes links or numbers itself.
3. `publish.py`: checks `feed.json`, copies the real title, link and numbers from the inputs by `ref`, drops anything it cannot match, and only replaces yesterday's report if there are at least 8 good items.
4. The report page reads the published file.
5. Scheduling: run it every morning. On Windows, Task Scheduler; on Mac, a scheduled job. Claude Code can run without a chat window (called headless mode). Explain that a daily run uses part of their plan's usage, and set a small budget.
6. Market numbers (optional): many free sources work without a key (for example the US Treasury's yield data and the St. Louis Fed's FRED data). If a source needs a free API key, it goes in a `.env` file (a hidden settings file) and never in chat, code or GitHub.

### Data shapes (sample data, made up)

Raw item (`raw-items.json`):

```json
{"id": "n1", "title": "Sample chip maker says demand is up 20%", "source": "Sample Wire",
 "url": "https://example.com/news/1", "published": "2026-11-11T00:15:00", "topic": "markets",
 "summary": "A short made-up summary of the story for practice."}
```

Report (`feed.json`):

```json
{"date": "2026-11-11", "sections": [{"key": "top", "items": [
  {"ref": "n1", "tier": 5, "why": "Why it matters to me", "summary": "Plain-words recap"}]}],
 "try_today": {"ref": "n3", "how": ["step 1", "step 2"], "tier": 5}}
```

### Accounts and connectors (tell the student as they come up)

- Version A: only the AI app. Web search inside the AI app is helpful; say whether their app has it.
- Version B: Claude Code (paid plan, check claude.com/pricing) and Python.
- Optional: a Gmail connector if they want the report as an email draft. Explain a connector is a permission for the AI to use one app, and that it should write a draft only, never send on its own.

### Make it yours

- A "number of the day" card.
- Video cards that jump to the exact minute worth watching.
- A weekly recap on Sunday.

### Done when

- The page shows the sample report with sections, the 5, 15, 30 switch, and a working link on every card.
- The student made one real edition from their own sources, every card with a real link.
