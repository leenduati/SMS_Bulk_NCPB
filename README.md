# NCPB Fertilizer SMS Sender

A simple, **100% browser-based** tool to send bulk SMS reminders to Kenyan farmers using the **SMSGate API**.

No server, no installation, no backend needed — just open the HTML file in a browser (or better: host it on GitHub Pages for free).

Designed especially for Nakuru NCPB fertilizer collection reminders, but can be used for any SMS broadcast campaign.

![Screenshot of the tool](https://via.placeholder.com/800x500.png?text=Screenshot+of+SMS+Sender+Interface)  
*(Add a real screenshot here later – take one when the tool is running)*

## Features

- Paste your full SMS message directly (no fixed template anymore)
- Paste many phone numbers at once (from Excel, WhatsApp, etc.)
  - One number per line, or separated by commas / spaces
  - Automatically cleans Kenyan numbers to international format (+2547xxxxxxxx)
- Real-time progress bar and live log of successes / failures
- Stop button to pause sending at any time
- Remembers where you left off (using browser localStorage) — resume after refresh
- 2.2-second delay between messages (safe for most SMS gateways)
- Very beginner-friendly code with **lots of comments** — easy for any IT person to understand or modify

## Important – How to Run It Correctly

**Double-clicking the file directly (file:///) will NOT work properly**  
→ Modern browsers block internet requests (like sending to SMSGate API) from local files for security reasons.

You have **two easy ways** to make it work:

### Option 1 – Recommended: Host on GitHub Pages (free forever)

1. Create a GitHub account (if you don't have one)
2. Create a new repository (e.g. `ncpb-sms-sender`)
3. Upload the file `smsncpb.html` to the repository
4. Go to **Settings → Pages**
5. Under "Source", choose **Deploy from a branch**
6. Select **main** (or gh-pages) branch and **/ (root)** folder → Save
7. Wait 1–2 minutes
8. GitHub will give you a link like:  
   https://yourusername.github.io/ncpb-sms-sender/smsncpb.html
9. Open that link in any browser — now it works perfectly!

### Option 2 – Quick test on your own computer

Install one of these free tools and run a tiny web server:

- **VS Code** + Live Server extension  
  → Right-click `smsncpb.html` → "Open with Live Server"

- **Python** (most computers already have it)  
  Open terminal/command prompt in the folder with the file and run:
  ```bash
  python -m http.server 8000
