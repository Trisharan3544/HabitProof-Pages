# HabitProof policy pages

This folder is ready to publish with GitHub Pages. It contains:

- `index.html` — landing page linking to both documents
- `privacy-policy.html` — Privacy Policy
- `terms-and-conditions.html` — Terms and Conditions
- `account-deletion.html` — signed-in website account deletion flow
- `policy.css` and `assets/habitproof-logo.png` — shared page styling and the app logo
- `firebase-config.js` — Firebase Web App config used by the deletion page

## Publish with GitHub Pages

1. Push this project to a GitHub repository.
2. In the repository, open **Settings → Pages**.
3. Under **Build and deployment**, choose **Deploy from a branch**.
4. Choose the branch you publish from (usually `main`) and the `/docs` folder, then save.
5. GitHub will show the published site URL. The policy URLs will be:
   - `https://<owner>.github.io/<repository>/privacy-policy.html`
   - `https://<owner>.github.io/<repository>/terms-and-conditions.html`

For a user or organization site repository named `<owner>.github.io`, the pages are at `https://<owner>.github.io/privacy-policy.html` and `https://<owner>.github.io/terms-and-conditions.html`.

## Enable account deletion

1. Replace the placeholders in `firebase-config.js` with the Firebase Web App config from Firebase Console → Project settings → Your apps. The config contains public client identifiers; do not place service account credentials in the site.
2. In Firebase Authentication settings, add your GitHub Pages domain (for example, `<owner>.github.io`) to **Authorized domains**. Enable the Google provider if users sign in with Google.
3. Deploy the `deleteOwnAccount` Cloud Function from the `functions` directory with `firebase deploy --only functions:deleteOwnAccount`.
4. Deploy the updated Android app to enable its profile deletion action. The website and app both use the same authenticated Cloud Function.

The in-app option is available from student and admin profiles. Students’ profiles, activity data, submissions, and proof photos are removed. To protect school and student records, an admin must transfer school management and resolve student records before deleting the account.
