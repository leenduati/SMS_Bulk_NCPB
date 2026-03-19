# NCPB Fertilizer SMS Sender

A simple, secure, browser-based tool to send bulk SMS reminders to Kenyan farmers about fertilizer collection days — built for the **National Cereals and Produce Board (NCPB)**.

This tool lets you paste a message and phone numbers, then sends the SMS through the official SMSGate API — all from a webpage anyone can open (no app installation needed).

### Why We Built This Tool

Originally, we had a Python script that worked perfectly in Google Colab — it sent messages reliably using SMSGate.

But when we tried to turn it into a nice webpage hosted on GitHub Pages (free, easy to share), it **stopped working** in the browser.  
The reason: modern browsers block direct API calls from websites for security reasons (called **CORS**). The SMSGate server said, "I don't know this website — blocked".

So we solved it properly — without using risky public proxies or changing SMSGate.

### What the Tool Does Now

- Users paste the SMS message (e.g., "Dear farmer, your collection day is Monday...")
- Paste many phone numbers (from Excel, WhatsApp, etc.)
- Numbers are automatically cleaned to correct the Kenyan format (+2547xxxxxxxx)
- Sends one message every 2.2 seconds (safe for the API)
- Shows live progress bar + log (green = success, red = failed)
- Can stop sending anytime
- Remembers where it stopped (even if the page is closed and reopened)
- If some numbers fail → a button appears to **download failed numbers as CSV**
- Looks professional with the NCPB logo at the top
- Has light/dark mode toggle (easy on the eyes)
- Fully works from any browser (phone or computer)

### How It Works (Behind the Scenes – Simple Version)

1. The webpage lives on GitHub Pages (free hosting) → link: https://leenduati.github.io/SMS_Bulk_NCPB/
2. When you click "Start Sending SMS", the browser sends the request to **our own private middleman server**
3. The middleman is a tiny Cloudflare Worker (free forever) → https://sms-proxy-ncpb.leenduati21.workers.dev/
4. The middleman forwards the request to the real SMSGate API (adds permission so browser allows it)
5. SMSGate sends the SMS → reply comes back through the middleman → shown in the log

This middleman solves the browser security problem cleanly and safely.

### Features Added Over Time

| Feature                          | Why we added it                          | Status     |
|----------------------------------|------------------------------------------|------------|
| Basic sending from webpage       | Make it easy to use without Colab        | Done       |
| Fix CORS (browser block)         | Original page failed in browser          | Done       |
| Own Cloudflare proxy             | Safe, free, no third-party dependency    | Done       |
| NCPB logo at top                 | Looks official and branded               | Done       |
| Download failed numbers as CSV   | Easy to follow up on bad numbers         | Done       |
| Soft dark mode toggle            | Better for eyes during long use          | Done       |
| Progress bar + live log          | See exactly what's happening             | Done       |
| Resume after refresh/stop        | No need to start over if interrupted     | Done       |

### How to Use the Tool

1. Open the link: https://leenduati.github.io/SMS_Bulk_NCPB/
2. Enter your SMSGate **username** and **password** (same as in Colab)
3. Paste the message you want to send
4. Paste phone numbers (one per line, or separated by comma/space)
5. Click **Start Sending SMS**
6. Watch the progress & log
7. If any numbers fail → click **Download Failed Numbers as CSV**
8. You can stop anytime with the red button

### Technical Details (for ICT team)

- Frontend: HTML + JavaScript + Tailwind CSS
- Hosting: GitHub Pages (free, automatic updates)
- SMS API: SMSGate Cloud Server (same endpoint as original Python script)
- CORS solution: Custom Cloudflare Worker proxy
  - URL: https://sms-proxy-ncpb.leenduati21.workers.dev/
  - Code: src/index.ts (TypeScript handler)
  - Config: wrangler.jsonc
- No database, no login, no server costs
- Security: Credentials are only used in the browser during sending — never saved or sent elsewhere

### How to Update the Tool

1. Edit the file `smsncpb.html` in GitHub (or locally)
2. Commit & push → GitHub Pages updates automatically (~1 minute)
3. If changing the proxy → redeploy Worker with `wrangler deploy.`

### Credits & Thanks

- Built with help from Grok (xAI)
- Original Code from Github from Brian Waweru
- Uses: Bootstrap (UI), Tailwind (styling), Cloudflare Workers (proxy)
- Inspired by the original Python script in Google Colab

Happy sending reminders to farmers! 🌾📱
