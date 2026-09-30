# Abbasia Sunday Crew — production Firebase package

This package is the existing Abbasia Sunday Crew app, kept on Firebase Authentication + Cloud Firestore, with a root `index.html` for Firebase Hosting/PWA installation.

## Firebase project
- Project: `abbasia-sunday-crew`
- Auth domain: `abbasia-sunday-crew.firebaseapp.com`
- Firestore: enabled by the app
- Realtime Database URL remains in the client config but is not used for shared app data.

## First-time Firebase setup

1. In Firebase Console → Authentication → Sign-in method, enable **Email/Password**.
2. Create the **first leader** manually in Authentication → Users.
3. Copy that user's UID.
4. In Firestore create `leaders/{UID}` with at least:
   - `username`: your leader username
   - `role`: `leader`
   - `language`: `ar`
5. Publish the included `firestore.rules`.
6. Deploy the folder with Firebase Hosting.

The app deliberately does **not** contain a service-account key or a secret that would allow anonymous users to become leaders.

## Firebase CLI deployment

From this folder:

```bash
firebase login
firebase use abbasia-sunday-crew
firebase deploy --only hosting,firestore:rules
```

After deployment, open the Hosting URL over HTTPS. PWA installation requires HTTPS (localhost is also suitable for local testing).

## What is already wired

- Firebase Auth with persistent browser sessions.
- Student login using generated login code + PIN.
- Leader login using username + password.
- Separate student and leader experiences.
- Firestore realtime listeners for shared class data.
- Quiet Time submissions/review.
- Memory verse submissions/review.
- Challenges/review.
- Attendance and streaks.
- Team + individual leaderboards.
- Point ledger and reversals.
- Rewards + redemption review.
- Announcements.
- Events + RSVP.
- Private student ↔ leader messaging.
- Notifications.
- Student profiles/avatars.
- Egyptian Arabic / English UI.
- PWA manifest, icons, and service worker.

## Important

The Firebase Web API key in the HTML is a normal client configuration value. Do not add a Firebase service-account JSON/private key to this web app. Security is enforced by Firestore Rules.
