# Waiting Room Check-In — Setup Guide

A free replacement for the $80/month waiting-room app. It's a single web page
(`index.html`) that runs on the front-desk iPad. Clients type their first name and
last initial, tap their therapist's photo, and the therapist's phone gets an
instant notification.

**Total ongoing cost: $0** (or a few cents per message if you choose real SMS).

---

## 1. Put the app online (free, one time, ~10 minutes)

The page needs a web address so the iPad can load it and remember its settings
reliably. GitHub Pages hosts it for free, forever:

1. Create a free account at https://github.com
2. Click **New repository**, name it `checkin`, leave it **Public**, and create it.
   (Public is fine — the file contains no names, photos, or phone numbers.
   All of that lives only on the iPad itself.)
3. Click **uploading an existing file**, drag `index.html` in, and click **Commit changes**.
4. Go to **Settings → Pages**, under "Branch" choose `main` and click **Save**.
5. After a minute your app is live at:
   `https://YOURUSERNAME.github.io/checkin/`

> Alternative: https://app.netlify.com/drop — drag the folder in, done. Also free.

## 2. Set up the iPad (~5 minutes)

1. Open the address above in **Safari** on the iPad.
2. Complete the one-time setup screen (practice name + admin password).
3. The app then shows a one-time **recovery code** (like `K3PM-7WQ2`).
   **Write both the password and the recovery code down.** If you ever forget
   the password, tap "Forgot password?" on the admin login and enter the code
   to set a new one. Lost the code too? You can generate a fresh one any time
   from Admin → Change admin password (as long as you can still log in).
3. Tap the **Share** button → **Add to Home Screen**. Opening it from the new
   home-screen icon gives you a clean, full-screen kiosk with no browser bars.
4. Optional but recommended — lock the iPad to the app so clients can't wander:
   **Settings → Accessibility → Guided Access** → turn on, set a passcode.
   Then open the check-in app and triple-click the side/home button to lock it in.

## 3. Add your therapists

1. On the kiosk screen, **tap the practice name 5 times quickly** — this opens
   the hidden admin login. Enter your admin password.
2. Tap **+ Add therapist**. Enter their name, add a photo (it's resized
   automatically), and pick how they get notified:

   | Method | Cost | What the therapist does |
   |---|---|---|
   | **ntfy push** (recommended) | Free, unlimited | Installs the free **ntfy** app, subscribes to their topic (one minute, once) |
   | **Telegram** | Free, unlimited | Messages your Telegram bot once; you pick them from "Detect recent chats" |
   | **Real SMS** (Textbelt) | ~a few ¢/text | Nothing — texts arrive like normal |

3. Use **Send test** to confirm their phone buzzes before saving.

### ntfy details (the recommended option)

- Therapist installs **ntfy** (App Store / Google Play, free, no account needed).
- In the app they tap **+ Subscribe to topic** and type the exact topic shown in
  the admin panel (e.g. `riverbend-counseling-dr-sarah-miller-4rg7g`).
- That's it. Every check-in now pops up on their phone like a text message.
- The random letters at the end of the topic keep it private — don't share topics
  publicly, and therapists shouldn't screenshot their subscription screen.

### Telegram details

1. In Telegram, message **@BotFather**, send `/newbot`, follow the prompts, and
   copy the bot token it gives you.
2. Paste the token into **Admin → Notification services → Telegram bot token**.
3. Each therapist opens Telegram, searches your bot's name, sends it "hi".
4. In the therapist's edit screen, tap **Detect recent chats** and tap their name.

### Real SMS details (Textbelt)

1. Buy credits at https://textbelt.com (pay as you go, no subscription).
2. Paste your key into **Admin → Notification services → Textbelt API key**.
3. Enter the therapist's mobile number with country code (e.g. `+15551234567`).

## 4. Back up your settings

Everything (therapists, photos, settings) is stored **on the iPad only** — in
Safari's storage for that page. Two things can erase it: clearing Safari
website data, or "erase all content" on the iPad.

So after setup: **Admin → Backup → Export backup**, and save that file somewhere
safe (email it to yourself). If anything is ever wiped, open the app, redo the
first-run screen, then **Import backup** — everything comes back, photos included.

## Privacy note (worth reading for a healthcare practice)

By default, notifications say **"A client has checked in for you (2:45 PM)"** —
no client name. This is deliberate: a message with no identifying information
isn't protected health information, so nothing sensitive ever passes through
the notification services (ntfy, Telegram, or SMS carriers — none of which sign
HIPAA Business Associate Agreements). Clients still type their name at the
kiosk; it appears only in the check-in log stored on the iPad itself, which is
the digital equivalent of a paper sign-in sheet (explicitly permitted under
HIPAA's incidental-disclosure rules).

**Admin → General → "What the notification says"** lets you include the
client's first name (or first name + last initial) instead. That's the same
thing most SMS check-in vendors send, but be aware it puts a client identifier
plus your practice name onto third-party services — if you want that, it's
worth a quick question to whoever advises you on HIPAA compliance.

## Daily use

Nothing to do. The iPad sits on the counter showing the check-in screen.
The admin panel shows the last 30 check-ins and whether each notification
was delivered, in case anyone says "I checked in but nobody came."
