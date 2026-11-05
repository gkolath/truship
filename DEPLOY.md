# Putting truship.org live on Firebase

Project: **truship-6a881**. The website saves each enquiry to Firestore (collection
`enquiries`) and can email you about each one. Do steps 1–2 first; the form starts
saving enquiries as soon as they're done, even before the site is on truship.org.

## 1. Create the database (console, 2 minutes)
1. Firebase console → **Build → Firestore Database → Create database**.
2. Choose **Start in production mode**.
3. Location: **asia-south1 (Mumbai)** is closest to Kochi. This can't be changed later.

## 2. Add the security rules (console, 1 minute)
1. **Firestore Database → Rules**.
2. Replace everything with the contents of `firestore.rules` from this folder, then **Publish**.

These rules let website visitors only *add* an enquiry with the expected fields.
Nobody can read, edit or delete enquiries from the website. You see them in the console
under **Firestore Database → Data → enquiries**.

## 3. Publish the website (one-time setup on your Mac)
1. Install Node.js (LTS) from https://nodejs.org.
2. In Terminal:
   ```bash
   npm install -g firebase-tools
   firebase login
   cd "/Users/georgedavidkolath/Portfolio - Website"
   firebase deploy
   ```
3. The site goes live at **https://truship-6a881.web.app**. To publish later changes, run
   `firebase deploy` again from the same folder. This also re-uploads the rules.

## 4. Connect truship.org
1. Console → **Build → Hosting → Add custom domain** → `truship.org` (and `www.truship.org`).
2. Add the DNS records Firebase shows wherever you bought truship.org.
3. HTTPS is set up automatically once DNS updates (minutes to a few hours).

## 5. Get an email for every enquiry (optional)
Needs the **Blaze (pay-as-you-go)** plan. At a consultancy's volume it stays at or near $0,
but a card is required.
1. Console → **Extensions → Trigger Email from Firestore → Install**.
2. Set **Email documents collection** to `enquiries`.
3. Set the **SMTP connection URI** for the account that sends the alerts, e.g. Zoho Mail or
   Gmail with an app password: `smtps://you@domain:APP_PASSWORD@smtp.zoho.in:465`.
4. Set **Default FROM address** to that same account.

Alerts go to **hello@truship.org**. To use another inbox, change it in both places, then deploy:
- `NOTIFY_TO` near the bottom of `index.html`
- the `d.to == '...'` line in `firestore.rules`

## How the form behaves
- If the enquiry is saved, the visitor sees "Thanks, we've got it."
- If Firestore can't be reached (e.g. the database isn't created yet, or the claude.ai
  preview blocks it), the visitor sees the "send this email" panel, so nothing is lost.
- A hidden spam trap discards most bot submissions without saving them.
