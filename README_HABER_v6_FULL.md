# HABER Neo-Next Pro v6 — Production Firebase Edition

This package keeps the original HABER v5 interface and adds production-oriented Firebase architecture.

## Included
- Firebase Authentication: Email/Password.
- Realtime Database: profiles, posts, comments, follows, notifications, chats, messages.
- Firebase Storage: post media and stories.
- Database + Storage security rules.
- Roles: user, moderator, admin.
- Admin Dashboard: users, roles, disable/enable, moderation, security notes.
- Messenger pagination and chat-membership authorization.
- Feed pagination using timestamp cursors.
- Lazy-loaded media and bounded queries for better performance.
- XSS-safe text rendering through HTML escaping.
- File size/type validation in the client plus Storage Rules.
- Firebase Hosting configuration.

## First-time Firebase setup
1. Open Firebase Console for the configured project.
2. Authentication → Sign-in method → enable Email/Password.
3. Realtime Database → create/enable the database.
4. Storage → enable Firebase Storage.
5. Replace `firebaseConfig` in `HABER_Neo_Next_Pro_v6_FULL.html` if you are using another Firebase project.
6. Deploy rules: `firebase deploy --only database,storage`.
7. Deploy hosting: `firebase deploy --only hosting`.

## First admin
For security, the client cannot promote itself. Create the first account normally, then in Firebase Console set:
`users/<AUTH_UID>/role = admin`
After the next login/refresh, the Admin Dashboard appears.

## Important migration note
v5 stored custom password hashes in Realtime Database. Firebase Authentication cannot safely accept those hashes from the browser. Existing users should reset/recreate their accounts in Firebase Auth, or be migrated with the Firebase Admin SDK on a trusted server/Cloud Function.

## Production recommendation
For a commercial deployment, keep Firebase API configuration in the frontend (Firebase web config is not a secret), but never expose Admin SDK credentials, service-account keys, or privileged server credentials.

## Files
- `HABER_Neo_Next_Pro_v6_FULL.html` — complete application.
- `public/index.html` — hosting entry point.
- `database.rules.json` — Realtime Database authorization rules.
- `storage.rules` — Storage validation rules.
- `firebase.json` — Hosting/database/storage deployment config.
- `.firebaserc` — Firebase project alias.
