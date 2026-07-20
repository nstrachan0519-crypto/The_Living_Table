The Living Table
A daily practice app for eating with gratitude — built with React, Vite, and Tailwind.
Run it on your own computer
You'll need Node.js installed first (the free download from that site, any recent version).
npm install     # downloads the pieces the app needs, once
npm run dev     # starts it at http://localhost:5173
Open that address in a browser. Changes you make to files in src/ show up instantly.
Push it to GitHub
git init
git add .
git commit -m "The Living Table"
git branch -M main
git remote add origin https://github.com/YOUR-USERNAME/YOUR-REPO-NAME.git
git push -u origin main
(Create the empty repo on GitHub's website first, then run the commands above from inside this folder.)
Make it a live website
Pushing to GitHub stores the files — it doesn't run them. Pick one of these to get a real link:
Option A — Vercel or Netlify (easiest)
Sign in with your GitHub account at vercel.com or netlify.com.
Click "New Project" / "Add new site" and pick this repo.
Leave the defaults — both recognize Vite automatically.
You get a live link in about a minute, and it updates itself every time you push.
Option B — GitHub Pages
In vite.config.js, uncomment the base: line and put your exact repo name in it, like base: "/the-living-table/".
Run npm run build — this creates a dist folder with the finished site.
Push dist to a branch named gh-pages (the gh-pages npm package automates this: npm i -D gh-pages, add "deploy": "gh-pages -d dist" to package.json's scripts, then npm run deploy).
In your repo's Settings → Pages, set the source to the gh-pages branch.
About the AI recipe generator — bring your own key
Inside Anthropic's own Claude.ai preview, the recipe generator talked to Claude for free, automatically. Outside that environment — including this repo — there's no shared free connection to any AI. Instead, the app has a "bring your own key" system built in:
Open the Kitchen tab → Recipes → Engine, pick Claude, ChatGPT, or Gemini.
Paste a free API key from that provider's own website (links are shown right in the app).
Your key is saved only in your own browser (localStorage) — it's never written into the code, never pushed to GitHub, and never sent anywhere except straight to that provider.
One honest security note: each engine's key is used directly from the browser, which means it's visible to anyone who inspects that browser's network traffic. This is safe only because it's each visitor's own personal key, on their own device, used for their own requests — never put a key you want to keep secret into this pattern. If you want the app to offer a free default AI to every visitor (instead of asking each person for their own key), the correct way is a small serverless function (a Vercel Function or Netlify Function both work well and have free tiers) that holds one key privately on the server and the app calls that — never put a key you want to protect directly into any file in this repo.
What's inside
src/App.jsx — the whole app: the philosophy, the five tabs, every feature.
src/storage.js — makes saving (journals, seeds, traditions, keys) work in a normal browser using localStorage.
src/main.jsx — the small file that starts everything.
src/index.css — loads Tailwind, the utility-class styling system the app's layout uses.
Everything a visitor saves — their journal, their seed library, their traditions, their API keys — lives only in their own browser. There's no shared database; each person's copy of the app is entirely their own.
