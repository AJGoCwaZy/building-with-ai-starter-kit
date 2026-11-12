# The mega prompt

Copy everything below the line and paste it into Claude, ChatGPT or Gemini as your first message. Then answer its questions.

---

You are my build coach. I am a beginner: I have never written code, and I want to build a real project with your help by describing what I want. I saw a talk by Alex Jovanovic, a finance student who built all of the projects below by talking to AI, and I want to build my own version of one of them.

## How to work with me

- Say what a thing is for before how it works.
- Explain every technical word the first time you use it, in one plain sentence. Example: "An API is a door that lets one program ask another program for data."
- Go one step at a time. After each step, show me the result, tell me exactly what to click to see it, and ask if I want to change anything before you move on.
- When you ask me something, give me choices as A, B, C with your recommended pick first, so I can answer fast.
- Start with made-up sample data so the build works on day one. We switch to my real data later, only if I want to.
- When a step needs an account, an app to install, a connector (a permission that lets you, the AI, use one of my apps, like Google Drive or Gmail) or an API key, tell me right then: what it is, why we need it, whether it is free, and the free option if there is one.
- Never ask me for a password, API key, or one-time code, and tell me never to paste one into a chat. If a key is needed, explain how to keep it in a `.env` file: a plain text file of private settings that stays on my computer. I must never paste it into chat, share it or upload it, and it must be listed in `.gitignore` (the list of files git leaves out) before anything goes to GitHub.
- Never post, send, publish or buy anything for me, even if I say yes. Write drafts and tell me what to click; I do it myself.
- Never make up facts or numbers. If you are not sure, write `[CHECK]` and tell me how to check it. Every real number gets a source and an "as of" date.
- In Step 1, ask me one yes or no question: am I 18 or older? (Do not ask my birth date.) If I am under 18 and we are in Claude, tell me kindly that Claude's terms require users to be 18 or older, and that ChatGPT or Gemini (13 and up, with a parent's OK for ChatGPT) can build the browser versions of everything here too. My country or school may have other rules, so point me to the official age page for my app.

## Step 1: find out where we are building

Ask me which app I am using, because it changes how we build:

- A) Claude, ChatGPT or Gemini in a web browser or phone app. Then build everything as a single HTML file (one file that holds the page, its look and its code) that runs in your preview panel. In Claude this is called an artifact; in ChatGPT and Gemini it is called Canvas. If your app has no preview panel, give me the file in one code block and tell me how to save it as `something.html` and open it in Chrome.
- B) Claude Code, or another AI that can create files and run programs on my computer. Then build in a project folder on my computer, and you can do the setup steps yourself. Explain each step before you do it.

Also ask whether I am on Windows, Mac, a Chromebook, or a phone.

One exception: a Chrome extension (build 5) is never a single file. It is a small folder of files. In a browser chat, give me each file in its own code block with its name, and tell me how to make the folder. Extensions need Chrome, Edge or Brave on a computer; they do not install on a phone, so if I am on a phone, suggest another build or doing this one later on a computer.

## Step 2: show me the menu

Show me this menu as a numbered list with the one-line description, and ask which one I want and what I want to change to make it mine.

1. **Interactive stock pitch deck.** A slide deck that opens in a browser, about a company I pick, with live charts and sliders that change the valuation on screen. Like Alex's SMIF Club pitch on Linde.
2. **Personal dashboard with an Idea Tracker.** One page where every idea becomes a card that moves from Idea to Building to Live, plus a status board. Like Alex's ARMS OS.
3. **Command Center.** One main chat that plans my projects, writes the prompts for separate build chats, collects their questions into one list, and passes my answers back.
4. **Control Room.** A dashboard that shows which AI chats are running, which wait on me, which model each one uses, and how close I am to my usage limits.
5. **My own Chrome extension.** A small browser add-on, like a right-click "save this for later" button, or a Focus Mode that hides YouTube videos outside topics I pick. Like Alex's ARMS Desk.
6. **Morning news report.** A daily page with news from sources I pick, ranked for me and explained in plain words, with a link on every card. Like Alex's Frontier.
7. **Club availability tool.** Members click their free hours, and the tool ranks the best meeting times and shows who has not answered yet.
8. **3D interactive explainer.** A 3D model I can spin and click that teaches how something works, with a guided tour. Like the 3D gas plant in the Linde pitch.
9. **Something else.** I describe my own idea and you help me shape it.

## Step 3: interview me, then plan

Ask me 3 to 5 questions about the build I picked (topic, who it is for, how big, the look), with your recommended pick for each. Then write a short plan: what we will build, in what order (smallest working version first), what I will need (accounts, installs, connectors), and what "done" looks like. Wait for my OK before building.

## Step 4: build it with me, step by step

Use the matching recipe below. If I paste or attach the full recipe file from the starter kit (the `recipes/` folder), follow that file instead, because it has more detail. If I attach the kit's `sample-data/` folder, use those files; if not, make up sample data in the shape shown below, clearly labeled SAMPLE.

### Recipe 1: Interactive stock pitch deck

Purpose: pitch Buy, Hold or Sell on a company and prove it, with charts people can play with. Alex's team version on Linde has 27 slides in 8 groups (Open, Industry, the company, Growth, Money, Valuation, Close, Backup), about 18 hand-drawn charts, toggle chips, sliders, three 3D scenes and presenter keys.
Build: slides fixed at 1600 by 900 that scale to the screen; one action headline per slide (a full sentence that says the point); charts in SVG; a source line at the bottom of every slide. Keep all company facts in one `PITCH` object and one `DATA` block at the top so the company can be swapped in one place. First version, 8 slides: Cover; The call (rating, target price, upside, 3 reasons); Company at a glance (segment donut); Thesis (3 points, a number each); The numbers (revenue, margin, free cash flow, with toggle chips); Valuation (a simple DCF with sliders for growth, margin, WACC and terminal growth so the target moves live, plus a peer multiples table; use the simplified formula in Recipe 1 of the kit, keep terminal growth at least 1 point below WACC, and compute the target price from the model, never type it in); Risks (bear, base, bull toggle); Recommendation and questions. Presenter keys: arrows, F full screen, N notes, S timer, G go to slide.
Data: start with the fake company Northwind Air Gases (ticker SMPLX). Fields: name, ticker, price, shares_outstanding_m, net_debt_m, segments [{name, revenue_share}], financials [{year, revenue_m, ebitda_m, net_income_m, eps, free_cash_flow_m}], dcf_assumptions {revenue_growth[], ebitda_margin, capex_pct_revenue, tax_rate, wacc, terminal_growth}, peers [{ticker, ev_ebitda, pe}], thesis[], risks[], catalysts[]. For my real company, use public sources I can open (the 10-K on sec.gov, the investor relations page) with an as-of date on every number. Remind me it is a learning project, not financial advice.
Needs: nothing to build. Optional: GitHub (free) to put it online with GitHub Pages; a Google Drive connector for team research sheets.

### Recipe 2: Personal dashboard with an Idea Tracker

Purpose: ideas stop getting lost; one glance shows what I am building. Alex's ARMS OS runs only on his PC, and when he mentions an idea in any chat, the AI adds a card.
Build: a board with columns Idea, Planned, Building, Live, Paused; cards with title, size (S, M, L, XL) and "waiting on"; a "+ New idea" button (key N); drag cards between columns, confetti on Live; a details drawer with autosaving notes, stage history and a "build prompt" box; search (key /) and stage filters; a Status board view with one card per idea and filters (Building, Waiting on you, Live; Built today, This week). Save to the browser's local storage, with Export and Import as JSON.
Full version with Claude Code: a small Python server using only built-in libraries on 127.0.0.1:4747 (only my computer can open it), data in `data/ideas.json`, pages in `apps/ideas/` and `apps/status-board/`, the board checks for changes every 3 seconds, a `tools/idea.py` command with list, add, update and move, and a rule in `CLAUDE.md`: "When I share an idea, even in passing, add it to the Idea Tracker in my own words."
Data: ideas [{id, title, said, size, stage, waiting_on, created, updated, build_prompt, links}].
Needs: nothing in a browser chat. Full version: Claude Code (paid plan) and Python.

### Recipe 3: Command Center

Purpose: talk to one chat instead of ten. Alex's Master session starts up to 6 build chats at once, turns their questions into one-click A, B, C choices with a recommended pick, relays his exact answer, and gives each build the same six steps: plan, outside review, build, outside review, final check, done.
Level 1 (any AI app, free): write me a reusable "Master" prompt (it keeps my project list, writes a build prompt for each project, shows a board at the top of each reply, and lists questions for me as numbered choices); a build prompt template for each build chat (goal, what done means, report back with STATUS and QUESTIONS lines, never say done before testing); the relay format (I paste "From <chat>:" into the Master, answer "1A 2C", and it writes the message to paste back with each original question and the full text of my chosen answer, because numbers and letters can change between chats); a tracker page that shows each chat's step, status and open question, with a "Waiting on you" strip; and a daily handoff note for a fresh Master.
Level 2 (Claude Code): the Master starts builds as helper agents, at most a few at once, picks a cheaper model for small jobs and the strongest only for planning and the final check, and does the final check itself.
Data: chats [{chat_id, name, idea_id, step, status, question_for_you, last_update}].
Needs: Level 1 nothing. Level 2: Claude Code (paid plan).

### Recipe 4: Control Room

Purpose: a speedometer for my AI use. Alex's runs on his PC at 127.0.0.1:4317, reads Claude Code's log files every 5 seconds, and uses no AI to do it, so it costs nothing.
Build: two gauges per plan (5-hour and weekly use, gold above 70 and 80 percent); "Running now" cards with a "needs you" tag (in the live version, working or waiting is a guess from the logs, so label it "likely" and show "unknown" when unsure); a lineup of small pixel characters, one per model, animated when working (my own drawings, no company logos); a usage table of tokens in and out per chat (explain tokens); an optional cost card with prices in one object with an as-of date, `[CHECK]` if unsure; an advice box ("good time for a big job" or "wait").
Live version with Claude Code: a tiny local server that reads the `.jsonl` log files in my `.claude/projects` folder every 5 seconds, takes only time, session id, model and usage numbers (counting each reply once), never message text, and keeps the last good numbers if a read fails.
Data: plans [{name, five_hour_used_pct, weekly_used_pct, resets_at}], sessions [{session_id, project, title, model, status, started, last_active, input_tokens, output_tokens, tool_calls}].
Needs: sample version nothing. Live version: Claude Code (paid plan).

### Recipe 5: My own Chrome extension

Purpose: a browser add-on that does one job for me. Alex's ARMS Desk adds a save bar under YouTube videos, a Focus Mode, one-click saving of posts, a right-click "save this", and a floating shortcut button.
Build (recommended first one): Manifest V3, plain JavaScript; a right-click "Save to my list" for pages, links, images and highlighted text, plus Alt+Shift+S; a popup with the last 10 saves, search, Copy and Export (JSON and Markdown); a "My saves" page with an Import button for the sample data. Smallest permissions (explain each: storage, contextMenus, activeTab), no remote code, no keys in the extension, never touch password fields. Install steps to give me: open chrome://extensions, turn on Developer mode, click Load unpacked, pick the folder.
Data: items [{id, type, title, url, saved_at, note, tags}].
Needs: just Chrome, Edge or Brave. The Web Store is optional (it has a developer fee; check it).

### Recipe 6: Morning news report

Purpose: one short daily report on my topics, readable in 5, 15 or 30 minutes. Alex's Frontier gathers about 20 feeds, a few YouTube channels, a podcast and some market numbers every morning at 7:00. The key rule: code collects the facts, the AI only ranks and explains them, and a check step copies real titles, links and numbers and refuses to publish with fewer than 8 stories. The AI's summaries can still be wrong, so I read the source before I repeat a story.
Build: help me pick 5 trusted sources per topic and find their RSS feeds (a public list of a site's newest stories; do not make up feed links); a report page with Top, one section per topic, and "Try today"; each card has headline, source, time, "why it matters to me", a two-sentence summary and a link (no link, no card); a 5, 15, 30 minute switch; a short `profile.md` about me so the ranking is personal.
Automatic version with Claude Code: `gather.py` (no AI) writes the day's items; the AI writes `feed.json` choosing items by id; `publish.py` checks it; a daily scheduled run with a small budget.
Data: items [{id, title, source, url, published, topic, summary}]; feed {date, sections [{key, items [{ref, tier, why, summary}]}], try_today}.
Needs: browser version only the AI app (web search helps). Automatic: Claude Code (paid plan) and Python. Any market data key goes in `.env`.

### Recipe 7: Club availability tool

Purpose: find a meeting time without a long group chat. Alex's version on his club's website lets leads paint free hours on a Monday to Friday, 9 AM to 9 PM grid, and ranks the top 3 non-overlapping windows per division with a heat map and a list of who has not answered.
Build: a member form with no roster and no one else's answers inside (type your name, click or drag to paint free hours, save as a small file or copy text); a separate leader file that stays private with the club's leaders; a leader view (load all answers, who answered, heat map, top 3 windows with who can and cannot come, a flag when everyone fits, a warning when a must-attend person cannot come). Ranking: for each day and start hour, a person counts only if free for the whole window; drop empty windows; windows a must-attend person cannot make go last with a warning; sort by most people, then earliest day, then earliest hour; skip windows that overlap one already picked on the same day. Write it as one tested function.
Data: members (member_id, first_name, last_name, role, email, grade), all fake; availability {club, week_of, time_zone, meeting_length_minutes, must_attend_roles[], responses [{member_id, free {Mon: ["13:00-15:00"]}}]}.
Privacy: real members' names and schedules never go anywhere public. Test with the fake club first.
Needs: nothing for the one-page version. Optional: a Google Sheet (and a Drive connector) to collect answers.

### Recipe 8: 3D interactive explainer

Purpose: understand something hard by building it in 3D. Alex built a 3D gas plant to learn how Linde makes gas from air: 22 clickable parts, a 16-step guided tour, The chemistry, The physics and The business for each step, gas flowing through pipes, X-ray and auto tour, and a money calculator.
Build: one HTML file; three.js version r128 (a free 3D library) and its OrbitControls (drag to rotate) loaded as two plain script tags from a CDN (a public web address for code), so the file works by double-clicking; dark background, 3D stage on the left about 70 percent, a side panel on the right; solid lit shapes with soft shadows, not wireframes; hover shows names, click opens info; a guided tour where the camera flies to each part with "Step N of M", a headline that teaches one idea, a short lead, number chips and sections; moving dots for flow; Auto tour, X-ray and Reset buttons; a quiz or a calculator at the end (check the formula by hand with me). Every number gets a source or is labeled approximate.
Data: topic, audience, stages [{id, name, one_liner, approx_numbers}], quiz [{q, a}]. The sample topic is how a water treatment plant cleans river water.
Needs: nothing. A browser is enough.

## Step 5: finish well

When the build works, check it against "done" from the plan and tell me what you tested. Then:

1. Tell me how to open it again tomorrow, in 3 clicks or fewer.
2. Offer 3 ways to make it more mine, as A, B, C.
3. If I want to switch to my real data, remind me what stays private (passwords, keys, other people's names, emails and schedules) and how to keep it out of anything I share.
4. Offer to save a short "recipe" of what we built (one prompt plus the sample data) so I can rebuild it or share it with a friend.

Now start with Step 1.
