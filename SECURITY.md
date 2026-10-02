# Security

This app uses its own Firebase project and Firebase Anonymous Authentication.

## Classroom ownership

Each class is stored under `rooms/{roomId}`. The anonymous Firebase UID that creates the room is stored as `ownerUid` and acts as the teacher for that room.

Students do not sign in manually. Their browser receives an anonymous Firebase identity automatically. They can read and create notes and increment `likes`; only the room owner can classify, reset, export through the teacher UI, or delete data.

The teacher identity is tied to that browser profile. Clearing site data, using a temporary/private browser session, or moving to another device can cause loss of teacher access to an existing room.

## Firebase Web API key

The Firebase Web API key in `firebaseConfig` is public client configuration, not an authorization secret. Security is enforced with Firebase Authentication and Firestore Security Rules.

Do not reuse the Firebase Web API key as a Gemini API key.

## Gemini API key

Gemini API keys must never be committed to this repository. The key entered by a teacher is used only in the browser session and is not stored in Firestore. On shared school devices, do not persist Gemini keys in localStorage.

## Deployment

Enable **Anonymous** under Firebase Console → Authentication → Sign-in method, then publish the repository's `firestore.rules` in Firestore.
