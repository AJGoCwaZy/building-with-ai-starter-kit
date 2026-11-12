# Building with AI: starter kit

Build your own version of what Alex Jovanovic showed in his "Building with AI" talk: an interactive stock pitch deck, a personal dashboard, a 3D explainer, a Chrome extension and more. You do not need to know how to code. You describe what you want, and your AI builds it with you, step by step, using made-up sample data so it works on day one.

## Start in 3 steps

1. **Open your AI.** Claude (claude.ai), ChatGPT (chatgpt.com) or Gemini (gemini.google.com). A free account is enough to start. Check the age rules below first.
2. **Paste the mega prompt.** Open [MEGA-PROMPT.md](MEGA-PROMPT.md), copy everything below the line, and paste it as your first message.
3. **Pick a build.** Your AI shows you the menu, asks what you want to change to make it yours, and builds it with you. It tells you along the way if you need an account, an app or a connector, and why.

Want more detail for one build? After step 2, also paste (or attach) its recipe from the `recipes/` folder. If your AI can read files, attach the matching `sample-data/` folder too.

## The builds

| # | Build | What you get | Recipe |
|---|---|---|---|
| 1 | Interactive stock pitch deck | A browser slide deck on a stock you pick, with live charts and valuation sliders (like the SMIF Club Linde pitch) | [01](recipes/01-stock-pitch-deck.md) |
| 2 | Personal dashboard | An Idea Tracker board and a status board (like ARMS OS) | [02](recipes/02-personal-dashboard.md) |
| 3 | Command Center | One chat that plans your projects and runs your other build chats | [03](recipes/03-command-center.md) |
| 4 | Control Room | A dashboard of your AI chats, models and usage limits | [04](recipes/04-control-room.md) |
| 5 | Chrome extension | Your own browser add-on, like a "save for later" button (like ARMS Desk) | [05](recipes/05-chrome-extension.md) |
| 6 | Morning news report | A daily report on your topics, ranked and explained (like Frontier) | [06](recipes/06-morning-news-report.md) |
| 7 | Club availability tool | Members click free hours, the tool finds the best meeting time | [07](recipes/07-club-availability.md) |
| 8 | 3D explainer | A 3D model you can spin that teaches how something works | [08](recipes/08-3d-explainer.md) |

**Easiest first builds:** 8 (3D explainer), 7 (availability tool), 2 (dashboard). They work fully inside a free browser chat.
**Need Claude Code for the full version:** 3 (Command Center, Level 2), 4 (Control Room, live version) and the automatic versions of 2 and 6. Each recipe also has a version that works in a browser chat.

## Sample data

Everything in [sample-data/](sample-data/) is made up: a fake company (Northwind Air Gases, ticker SMPLX), a fake club with fake members (emails end in example.com), fake headlines, fake chats and fake usage numbers. See [sample-data/README.md](sample-data/README.md). Swap in your own data only when you are ready, and keep private data private.

## Age rules (as of November 11, 2026)

| AI app | Minimum age | Source |
|---|---|---|
| Claude | 18 or older | [Anthropic Consumer Terms](https://www.anthropic.com/legal/consumer-terms) |
| ChatGPT | 13 or older; ages 13 to 17 need a parent's or guardian's permission | [OpenAI: age requirements](https://help.openai.com/en/articles/8313401-age-requirements-for-chatgpt) |
| Gemini | 13 or older in the US (18 in some countries); under 13 only with a parent through Family Link | [Google Gemini help](https://support.google.com/gemini/answer/16109150?hl=en) |

**Under 18:** use ChatGPT or Gemini, with a parent's OK. The browser version of every build works there too (the automatic versions that need Claude Code do not). Rules change, so check the links above before you sign up, and follow your school's AI policy.

## What it costs

- **Free to start.** Claude, ChatGPT and Gemini all have free plans that can build single-page apps you can see and click (Claude calls them artifacts; ChatGPT and Gemini call it Canvas). Free plans have daily limits; if you hit one, come back later.
- **Free tools.** Chrome, Python, GitHub and GitHub Pages are free for this kind of use.
- **Paid, optional.** Claude Code (the version of Claude that works in a folder on your computer) needs a paid Claude plan or pay-as-you-go API credits, not the free plan (as of November 11, 2026). Check current plans at [claude.com/pricing](https://claude.com/pricing). Publishing an extension to the Chrome Web Store has a one-time developer fee; you do not need the store to use your own extension.

## Stay safe

- **Never paste a password, API key or one-time code into any AI chat.** If a build needs a key, it goes in a `.env` file: a plain text file of private settings on your computer. Never share or attach it. This kit's `.gitignore` already lists `.env`, which tells git to leave it out, but only if the file was never added to git before; your AI can check that with you.
- **Other people's info is private.** Do not paste classmates' or club members' names, emails, phone numbers or schedules into public places or GitHub. Test with the sample data.
- **Check facts.** AI can be wrong. Every real number should have a source and a date. This kit is for learning, not financial advice.
- **You stay in charge.** The mega prompt tells your AI never to post, send, publish or buy anything for you, even if you say yes. It writes drafts; you click.

## What is in this folder

```
MEGA-PROMPT.md      the one prompt to copy and paste
recipes/            one detailed prompt per build, each works on its own
sample-data/        made-up data so every build runs on day one
LICENSE             MIT: use it, change it, share it
```

## Credits

Built by Alex Jovanovic (FIU, SMIF Club and the Financial Markets Society) with Claude. The personal "agentic OS" idea behind ARMS OS came from Jay E (RoboNuggets) on YouTube. All sample data is made up.

License: [MIT](LICENSE).
