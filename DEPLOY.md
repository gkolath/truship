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

## 5. Email for every enquiry (Web3Forms)
Each enquiry is emailed to **hello@truship.org** through Web3Forms (free plan, form
"Truship website enquiries", account hello@truship.org). The access key is `WEB3FORMS_KEY`
near the bottom of `index.html`; it is a public key and is safe in client-side code.
Firestore still keeps a backup copy of every enquiry. The Firebase Trigger Email extension
is not used (it needs the Blaze plan and Firebase Extensions shut down on 31 March 2027).

## How the form behaves
- If the email to hello@truship.org is sent, the visitor sees "Thanks, we've got it."
- If Web3Forms can't be reached, the visitor sees the "send this email" panel, so nothing
  is lost.
- A hidden spam trap discards most bot submissions without saving them.
