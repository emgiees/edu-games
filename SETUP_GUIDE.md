# Educational Games Online Platform - Setup Guide

## Overview
This platform enables real-time online multiplayer for your Accounting and Finance educational games, with a Teacher Dashboard to monitor student progress.

## Features
- **Teacher Dashboard**: Create sessions, monitor progress in real-time, export results
- **Student Mode**: Join sessions with a code, compete on live leaderboard
- **Real-time Sync**: See student answers and scores update instantly
- **Activity Feed**: Track who answered what and when
- **Export Results**: Download CSV of all student scores and progress

---

## Step 1: Create a Firebase Project (Free)

1. Go to [Firebase Console](https://console.firebase.google.com/)
2. Click **"Create a project"**
3. Enter a project name (e.g., "my-edu-games")
4. Disable Google Analytics (optional, not needed)
5. Click **Create project**

---

## Step 2: Enable Realtime Database

1. In Firebase Console, click **"Build"** → **"Realtime Database"**
2. Click **"Create Database"**
3. Select a location (choose closest to you, e.g., "europe-west1")
4. Select **"Start in test mode"** (for initial setup)
5. Click **"Enable"**

### Important: Set Security Rules
After testing, update your database rules. Go to **Realtime Database → Rules**:

```json
{
  "rules": {
    "sessions": {
      "$sessionId": {
        ".read": true,
        ".write": true
      }
    }
  }
}
```

For production, you may want stricter rules (contact me for help).

---

## Step 3: Get Your Firebase Config

1. In Firebase Console, click the **gear icon** → **"Project settings"**
2. Scroll down to **"Your apps"**
3. Click **"Add app"** → Select **Web** (</> icon)
4. Enter a nickname (e.g., "edu-games-web")
5. Click **"Register app"**
6. Copy the `firebaseConfig` object shown

It looks like this:
```javascript
const firebaseConfig = {
  apiKey: "AIzaSyD...",
  authDomain: "my-edu-games.firebaseapp.com",
  databaseURL: "https://my-edu-games-default-rtdb.europe-west1.firebasedatabase.app",
  projectId: "my-edu-games",
  storageBucket: "my-edu-games.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123456789:web:abc123..."
};
```

---

## Step 4: Configure the App

### Option A: Edit the built file (Quick)
1. Open `dist/assets/index-*.js` in a text editor
2. Search for `YOUR_API_KEY`
3. Replace all the placeholder values with your Firebase config

### Option B: Edit source and rebuild (Recommended)
1. Open `src/App.jsx`
2. Find the `FIREBASE_CONFIG` object near the top
3. Replace with your actual values:
```javascript
const FIREBASE_CONFIG = {
  apiKey: "AIzaSyD...",
  authDomain: "my-edu-games.firebaseapp.com",
  databaseURL: "https://my-edu-games-default-rtdb.europe-west1.firebasedatabase.app",
  projectId: "my-edu-games",
  storageBucket: "my-edu-games.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123456789:web:abc123..."
};
```
4. Run `npm run build` to rebuild

---

## Step 5: Deploy

### Option 1: GitHub Pages
1. Create a new repository on GitHub
2. Upload the contents of the `dist` folder
3. Enable GitHub Pages in Settings → Pages
4. Access at `https://username.github.io/repo-name/`

### Option 2: Firebase Hosting (Recommended)
1. Install Firebase CLI: `npm install -g firebase-tools`
2. Run: `firebase login`
3. Run: `firebase init hosting`
   - Select your project
   - Set public directory to `dist`
   - Configure as single-page app: Yes
4. Run: `firebase deploy`

### Option 3: Netlify Drop
1. Go to [app.netlify.com/drop](https://app.netlify.com/drop)
2. Drag and drop the `dist` folder
3. Get instant URL

---

## How to Use

### As a Teacher:
1. Open the app
2. Select **Teacher**
3. Enter your name
4. Choose **Accounting** or **Finance** game
5. Click **Create Session**
6. Share the 6-letter code with students
7. Monitor progress in real-time on your dashboard
8. Click **Export Results** to download CSV when done

### As a Student:
1. Open the app (same URL as teacher)
2. Select **Student**
3. Enter your name
4. Enter the session code from your teacher
5. Click **Join Session**
6. Complete scenarios and watch the live leaderboard!

---

## Troubleshooting

### "Session not found"
- Check the code is exactly 6 characters
- Make sure the teacher created the session first
- Try refreshing the page

### Changes not syncing
- Check your internet connection
- Verify Firebase config is correct
- Check browser console for errors (F12)

### Database errors
- Make sure Realtime Database is enabled
- Check security rules allow read/write
- Verify the databaseURL includes the correct region

---

## Free Tier Limits

Firebase free tier includes:
- 1 GB storage
- 10 GB/month downloads
- 100 simultaneous connections

This is plenty for classroom use (50+ students per session).

---

## Need Help?

Contact your instructor or check:
- [Firebase Documentation](https://firebase.google.com/docs)
- [Firebase Console](https://console.firebase.google.com/)

