# Firebase setup

1. In the [Firebase console](https://console.firebase.google.com/), create a project and register a **Web app**.
2. Copy its configuration values into a new `.env` file in this project. Use `.env.example` as the template.
3. In **Authentication → Sign-in method**, enable **Google**.
4. In **Firestore Database**, create a database. For the initial setup, select Production mode and replace its rules with:

```text
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /users/{userId}/habits/data {
      allow read, write: if request.auth != null && request.auth.uid == userId;
    }
  }
}
```

5. Run `npm run dev`, then use **Continue with Google**. Use that same Google account on every device. Wellness PDFs and other uploaded files stay only in the browser where they were added; no Firebase Storage account is required.

For a deployed app, add its domain in **Authentication → Settings → Authorized domains**.
