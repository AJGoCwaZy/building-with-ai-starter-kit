# Recipe 08: A 3D interactive explainer (like the Air Separation model in the Linde pitch)

> Paste this whole file into your AI chat. It works on its own. If your AI can read files, also give it `sample-data/explainer/topic.json`.

---

## Instructions for the AI

You are helping a beginner build a 3D model they can spin in the browser that teaches how something works, step by step. Treat them as someone who has never coded. Explain every new word the first time you use it. Go one step at a time. Never ask for a password, API key or one-time code.

### Rules for every build in this kit

- If the sample data files are not attached, create the sample data yourself in the shape shown in this recipe, clearly labeled SAMPLE, and put it inside the HTML file so the page works without loading other files.
- If your app has no preview panel, give the whole file in one code block and tell the student how to save it as `name.html` (in Notepad or TextEdit, "Save as", type the name with `.html` at the end) and open it in Chrome.
- Never post, send, publish or buy anything for the student, even if they say yes. Write drafts and tell them what to click; they do it themselves.
- Never ask for a password, API key or one-time code. If a key is needed later, it goes in a `.env` file: a plain text file of private settings that stays on the student's computer. It must never be pasted into chat, shared, attached or uploaded, and it must be listed in `.gitignore` (the list of files git leaves out) before anything goes to GitHub.

### What this is for (say this to the student first)

The best way to understand something hard is to build it. Alex did not understand how Linde makes gas out of air, so he had AI build a 3D model of a whole gas site to learn it, and then used it in his stock pitch. You can rotate it, click any part, take a guided tour, and move sliders to see how the company makes money.

His model, "The Air Separation Business", has 22 labeled parts you can click (air intake, the main compressor, the cold box, the columns, storage tanks, a tanker bay, and customers like a hospital and a chip factory), a 16-step guided tour where the camera flies to each part with a one-line headline ("The raw material is free", "Compression is where the power goes", "The contract is the moat"), a side panel with The chemistry, The physics and The business for each step, moving dots that show gas flowing through the pipes, an X-ray button, an auto tour, and a money calculator with sliders. It is one HTML file.

### First, ask the student these 4 questions (with a recommended pick)

1. What should it explain? A) something from a class you find hard: a plant cell, a volcano, the heart (recommended) B) how a company makes its product, for a stock pitch C) a machine or process (a water plant, a car engine, a data center) D) start with the sample: a water treatment plant.
2. Who is it for? A) your grade (recommended) B) younger kids C) a club or class presentation.
3. How many steps? A) 6 steps (recommended for a first build) B) 12 to 16 like Alex's.
4. A calculator or quiz at the end? A) a short quiz (recommended for school topics) B) a money calculator (for a business topic) C) none.

### Facts rule

Every number gets a source and, for anything that changes, an "as of" date. Simplified numbers are labeled "approximate". If you are not sure of a fact, mark it `[CHECK]` and tell the student. For a school topic, suggest checking against their textbook.

### How to build it

One single HTML file, made to run in the chat's preview panel (Claude: artifact; ChatGPT and Gemini: Canvas) or by double-clicking the file.

1. **Library:** three.js version r128 (a free library for 3D in the browser) and its OrbitControls (lets you drag to rotate and scroll to zoom), loaded from a CDN (a public web address for code) as two plain `<script>` tags, not modules, so the file works by double-clicking. Explain both words in one line each.
2. **Layout:** dark background, the 3D stage on the left (about 70 percent of the width), a scrolling side panel on the right. On a phone, the panel goes under the stage.
3. **The model:** solid, lit 3D shapes (boxes, cylinders, spheres put together), with soft shadows. Not wireframes. Each part has a name and a clear color by type, with a small color legend.
4. **Click and hover:** hover shows the part's name; clicking a part opens its info in the panel.
5. **Guided tour:** a step bar with Previous and Next. Each step flies the camera smoothly to its part and shows: "Step N of M", a headline that teaches one idea, a two-sentence lead, two or three number chips, and short sections (for example How it works and Why it matters).
6. **Flow:** small moving dots along pipes or paths to show what moves where.
7. **Buttons:** Auto tour (moves every 8 seconds, stops when you touch anything), X-ray (see inside), Reset view.
8. **The end:** a quiz from `topic.json`, or a calculator with sliders whose formula you check by hand with the student, showing the math once.
9. **Polish:** respect the "reduce motion" setting (no auto spin for people who turn motion off), and make sure it works at small widths.

Optional for a deck: wrap the scene in one function `mountExplainer(container, options)` that returns `goStep`, `pause` and `destroy`, so it can be placed live inside a slide deck (see Recipe 01).

### Data shape (sample data, made up)

```json
{"topic": "How a water treatment plant cleans river water", "audience": "10th grade",
 "stages": [{"id": "intake", "name": "Intake", "one_liner": "Pumps pull river water in through screens that stop sticks and fish.",
   "approx_numbers": "screen gaps about 1 cm (approximate)"}],
 "quiz": [{"q": "Why add a chemical in coagulation?", "a": "So tiny dirt bits clump together and sink."}]}
```

A step in the code can look like: `{chapter, headline, lead, chips: [], sections: [{title, body}], target: "part name"}`.

### Accounts and connectors

None. A browser is enough. If the page is opened offline, the CDN cannot load. For offline use, save both files (`three.min.js` and `OrbitControls.js`, version r128) next to the HTML file and point the two script tags at them; test it by double-clicking with the internet off.

### Make it yours

- More steps, grouped into chapters.
- A "follow the dollar" view for a company: where the money comes in and goes out.
- Screenshots of each step for slides.

### Done when

- The 3D model loads, rotates with the mouse, every part shows its name on hover, and the guided tour moves through every step.
- The quiz or calculator works, and every number has a source or is marked approximate.
