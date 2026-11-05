# Truship

Website for [Truship](https://truship.org), a software delivery consultancy covering development, test automation, release management and AI agents.

## What's here

| Path | Purpose |
|---|---|
| `index.html` | The whole site: one page with its own CSS and JavaScript, no build step |
| `logo/` | Logo files (SVG and PNG, light and dark) |
| `firestore.rules` | Security rules for the contact form's `enquiries` collection |
| `firebase.json`, `.firebaserc` | Firebase Hosting and Firestore settings for project `truship-6a881` |
| `DEPLOY.md` | Step-by-step setup and deployment notes |

## Contact form

The form saves each enquiry to Firestore (`enquiries`). The rules allow create-only with a fixed set of fields, so nobody can read or change enquiries from the website. If saving fails, the visitor gets a ready-to-send email instead.

## Run locally

```bash
python3 -m http.server 8765
```

Then open http://localhost:8765. Submitting the form from localhost writes a real enquiry to Firestore.

## Deploy

```bash
firebase deploy --only hosting,firestore:rules
```

Hosting is live at https://truship.org and https://truship-6a881.web.app.
