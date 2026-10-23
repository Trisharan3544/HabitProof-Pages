# HabitProof release checklist

## Build and signing

- Create an upload keystore and keep it outside version control.
- Copy `keystore.properties.example` to `keystore.properties`, then supply the real local keystore path and credentials.
- Build the release app bundle with `./gradlew bundleRelease`.
- Upload the generated `.aab` to a closed Play testing track before production.

## Firebase production project

- Replace `app/google-services.json` with the production Firebase Android app configuration.
- Deploy `firestore.rules`, `storage.rules`, and indexes with the Firebase CLI.
- Enable Authentication providers used by the app and add the release signing SHA-1/SHA-256 for Google sign-in.
- Confirm Crashlytics receives a test crash and Analytics receives a non-sensitive test event.

## Security and privacy blockers

- The current Firestore rules intentionally let every signed-in user read users, schools, classes, activities, instances, and submissions. This is appropriate only for the MVP. Before launch, replace these with school-scoped role checks backed by trusted server-side authorization (for example, Firebase custom claims or Cloud Functions).
- The current Storage rules similarly allow every signed-in user to read profile, school, and submission files. Restrict reads to the file owner and authorized school admins before launch.
- Publish a privacy policy that discloses student data, proof photos, retention, Firebase processors, and deletion/contact procedures.

## Play policy and validation

- Confirm that exact alarms, full-screen notifications, and battery-optimization requests are permitted for the app's declared Play use case; remove any capability that does not meet the policy.
- Test sign-up, sign-in, password reset, school/class joining, capture/upload, photo expiry, offline recovery, reminder delivery, and account deletion on Android 8 through 14.
- Verify accessibility labels, font scaling, dark mode behavior, and no-network error recovery on physical devices.
