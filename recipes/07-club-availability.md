# Recipe 07: A club availability tool that finds the best meeting time

> Paste this whole file into your AI chat. It works on its own. If your AI can read files, also give it `sample-data/club/`.

---

## Instructions for the AI

You are helping a beginner build a tool for their club: every member clicks the hours they are free, and the tool ranks the best meeting times and shows who has not answered yet. Treat them as someone who has never coded. Explain every new word the first time you use it. Go one step at a time. Never ask for a password, API key or one-time code.

### Rules for every build in this kit

- If the sample data files are not attached, create the sample data yourself in the shape shown in this recipe, clearly labeled SAMPLE, and put it inside the HTML file so the page works without loading other files.
- If your app has no preview panel, give the whole file in one code block and tell the student how to save it as `name.html` (in Notepad or TextEdit, "Save as", type the name with `.html` at the end) and open it in Chrome.
- Never post, send, publish or buy anything for the student, even if they say yes. Write drafts and tell them what to click; they do it themselves.
- Never ask for a password, API key or one-time code. If a key is needed later, it goes in a `.env` file: a plain text file of private settings that stays on the student's computer. It must never be pasted into chat, shared, attached or uploaded, and it must be listed in `.gitignore` (the list of files git leaves out) before anything goes to GitHub.

### What this is for (say this to the student first)

Finding a time that works for a whole club usually means a long group chat. This tool replaces that: one grid, everyone paints their free hours, and the tool says "Wednesday 4 to 6 PM works for 8 of 10, including the President and Treasurer".

Alex's version lives on his club's website for the SMIF Club at FIU. Division leads paint the hours they can teach next semester on a Monday to Friday, 9 AM to 9 PM grid (click or drag, works on a phone). The President sees who has answered, a heat map of how many people are free in each hour, and the top 3 two-hour windows for each division, never two that overlap on the same day. It flags when one window fits everyone. Each lead sees only their own division. Reminder emails exist but are off unless the President turns them on.

### Member privacy rule (very important)

Real members' names, emails and schedules are private. Build and test with the made-up sample club first. When the student uses it for real, real data stays out of any public place (no GitHub, no screenshots posted online), and only the people running the club can see everyone's answers.

### First, ask the student these 4 questions (with a recommended pick)

1. Which version? A) one HTML page, I collect answers by sharing the page (recommended to start) B) answers saved to a Google Sheet C) a real website with sign-in.
2. Grid? Suggest Monday to Friday, 9 AM to 9 PM, 1-hour blocks.
3. Meeting length? A) 1 hour (recommended) B) 2 hours like Alex's teaching sessions.
4. Who must attend? Suggest the President and Treasurer.

### Version A: one HTML page (free)

Build one single HTML file (Claude: artifact; ChatGPT and Gemini: Canvas).

Make two separate files, so private data never travels with the form:

1. **Member form (`availability-form.html`), the one you share:** no member list and no one else's answers inside. The member types their name, then clicks or drags across the grid to paint free hours. A note box. A Save button that downloads their answer as a small JSON file, or copies it so they can send it to a leader privately.
2. **Leader page (`availability-leader.html`), kept private by the club's leaders:** load the member list and all answers (drag the files in, or paste them). Nothing is saved inside the file. Show:
   - who answered and who has not yet,
   - a heat map: each hour colored by how many people are free,
   - the top 3 windows, never two overlapping on the same day,
   - for each window, who can come and who cannot,
   - a flag when a window fits everyone, and a warning when a must-attend person cannot make it.
3. Load the sample club so the leader page is full on day one. Embed the sample data only in the practice copy, never real answers.

### The ranking method (explain it to the student in plain words)

1. For each day and each start hour, look at the whole meeting window (for example 4 to 6 PM).
2. A person counts as free only if they are free for the entire window.
3. Drop windows nobody can make. Windows a must-attend person cannot make go last, with a warning.
4. Sort by most people free, then earliest day, then earliest hour.
5. Pick the top 3, skipping any that overlap one already picked on the same day.

Write this as one small, tested function, and test it on the sample data together: with the sample club and a 1-hour meeting, Wednesday 4 PM should be at or near the top.

### Version B: answers in a Google Sheet

Answers go to a Google Form or Sheet that only the club's leaders can open; the leader page reads the exported sheet. If the student's AI has a Google Drive connector, explain: a connector is a permission for the AI to read one app; the AI can then read the sheet and rank the times. Only the club leaders should have access to that sheet.

### Version C: a real website (advanced)

A small web app with sign-in so each member edits only their own answers and only leaders see everyone. Alex's version uses a database (Supabase) with rules so no page reads the tables directly. This needs accounts (a database and a host) and more care with privacy; suggest it only after Version A works.

### Data shapes (sample data, made up)

`members.csv`: `member_id,first_name,last_name,role,email,grade` (all fake, emails end in example.com).

`availability.json`:

```json
{"club": "Sample Investing Club", "week_of": "2026-11-16", "time_zone": "America/New_York",
 "slot_minutes": 60, "meeting_length_minutes": 60, "must_attend_roles": ["President", "Treasurer"],
 "responses": [{"member_id": "M01", "free": {"Mon": ["13:00-15:00"], "Wed": ["16:00-18:00"]}}]}
```

Times are whole hours, on a 1-hour grid. Inside the code, store one hour as day number times 100 plus the start hour (Monday is 1, Friday is 5), so 209 means Tuesday 9 to 10 AM. The grid runs from 9 (9 AM) to 20 (8 to 9 PM), and a meeting window must end by 21 (9 PM).

### Make it yours

- Pick the week, not just the days.
- "Remind people who have not answered": the tool writes the reminder message, the student sends it.
- Export the chosen time as a calendar file (.ics) members can add with one click.

### Done when

- A member can paint hours and save them; the leader view loads the sample club and shows the heat map, the top 3 windows, and who has not answered.
- The ranking test on the sample data passes.
