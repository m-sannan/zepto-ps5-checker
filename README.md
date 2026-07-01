# Zepto PS5 Stock Checker — Bangalore

Scans 66 Bangalore locations on Zepto and alerts you the moment a PS5 is in stock.

Built and shared by u/[your_username] on r/bangalore.

---

## What you need

- A Mac or Windows PC
- Python 3 installed
- A Zepto account (logged in on Chrome)

---

## Step 1 — Install Python 3

**Mac:**
Check if you already have it:
```
python3 --version
```
If not, download from: https://python.org/downloads

**Windows:**
Download from: https://python.org/downloads
During install, tick **"Add Python to PATH"**

---

## Step 2 — Install the one dependency

Open Terminal (Mac) or Command Prompt (Windows) and run:
```
pip3 install requests
```

---

## Step 3 — Get your Zepto cookie

This is your personal login session. **Do not share this with anyone.**

1. Open **Chrome** → go to **zeptonow.com** → log in
2. Press **F12** to open DevTools
3. Click the **Application** tab at the top
4. In the left sidebar: **Storage → Cookies → https://www.zepto.com**
5. You'll see a list of cookies

Now get them all at once — paste this into the Chrome address bar and press Enter:
```
javascript:void(document.location='data:text/plain,'+document.cookie)
```
A plain text page opens with all your cookies. **Select all → Copy.**

---

## Step 4 — Create cookie.txt

In the same folder as `zepto_ps5_checker.py`, create a new file called:
```
cookie.txt
```
Paste your copied cookie string into it. Save. That's it.

**Your cookie stays on your machine and is never sent anywhere except Zepto's own servers.**

---

## Step 5 — Validate your setup

Run this first to confirm everything is working:

**Mac:**
```
python3 zepto_ps5_checker.py --test
```
**Windows:**
```
python zepto_ps5_checker.py --test
```

You should see `🔥 IN STOCK!` for most areas (it's checking Paper Boat, a common item).  
If you see that — your setup is working correctly.

---

## Step 6 — Run the PS5 scan

```
python3 zepto_ps5_checker.py
```

Takes about 5–6 minutes to scan all 66 locations. Results print live.  
If PS5 is found, your Mac will also show a notification with a sound.

---

## Run it overnight (recommended)

PS5 stock appears in short windows. Running repeatedly gives you the best chance.

**Mac — keep running every 30 mins:**
```
caffeinate -i &
while true; do
    python3 zepto_ps5_checker.py
    echo "--- Waiting 30 mins before next scan ---"
    sleep 1800
done
```

**Windows — keep running every 30 mins:**
```
:loop
python zepto_ps5_checker.py
timeout /t 1800
goto loop
```

Press **Ctrl + C** to stop at any time.

---

## Cookie expires in ~1 hour

Zepto session tokens are short-lived. If you see:
```
⚠️  Cookie expired — refresh cookie.txt and restart
```
Just repeat Step 3, paste the new cookie into `cookie.txt`, and re-run.

---

## Flags

| Flag | What it does |
|------|-------------|
| `--test` | Runs on Paper Boat to validate your setup |
| `--debug` | Shows the exact signal string that triggered each result |

---

## FAQ

**Is this safe to run?**  
Yes. The script only reads Zepto's product pages — the same thing your browser does. It adds delays between requests to avoid hammering their servers.

**Will my account get banned?**  
Unlikely. The script mimics normal browser behaviour and runs slowly. That said, use it responsibly.

**Can I add more locations?**  
Yes — open the script and add entries to `GROUP_A` or `GROUP_B` in the format:
```python
("Area Name", latitude, longitude),
```

**Cookie not working?**  
Make sure you're logged in on Zepto before copying the cookie. Grab a fresh one and paste it into `cookie.txt`.

---

## Files

```
zepto_ps5_checker.py   ← the script
cookie.txt             ← your personal cookie (create this yourself, never share it)
README.md              ← this file
```
