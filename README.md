# KWK Prize Wheel — iPad kiosk

The prize wheel / slot machine as an iPad Home Screen app: full screen, no Safari bar, no Claude bar.
Prizes, odds, stock and counts sync live across every booth iPad through a free Firebase project.

## 1. Create the Firebase project (about 5 minutes, one time)

1. Go to https://console.firebase.google.com and sign in with a Kode With Klossy Google account.
2. **Add project** → name it `kwk-prize-wheel` → you can turn Google Analytics off → **Create project**.
3. **Build → Firestore Database → Create database** → pick a US location → **Start in production mode**.
4. Still in Firestore, open the **Rules** tab. Replace everything with the contents of `firestore.rules`,
   change `booth@kodewithklossy.com` to the booth account email you'll use in step 5, and **Publish**.
5. **Build → Authentication → Get started → Email/Password → Enable → Save**.
   Then **Users → Add user**: the booth email and a password. This is what staff type on each iPad once.
6. **Project settings** (gear icon) → **Your apps** → the **</>** (Web) button → nickname `kiosk` → **Register app**.
   Firebase shows a `firebaseConfig = { ... }` block. Copy those values into `firebase-config.js`,
   replacing each `PASTE_...` placeholder.

## 2. Put it on GitHub Pages

1. On github.com, create a new repository (for example `kwk-prize-wheel`). Public is fine; nothing secret is in these files.
2. **Add file → Upload files** → drag in everything in this folder (including `firebase-config.js` after you edit it) → **Commit**.
3. **Settings → Pages** → Source: **Deploy from a branch** → Branch: `main`, folder `/ (root)` → **Save**.
4. After a minute or two, the page shows your site address, like `https://YOUR-ORG.github.io/kwk-prize-wheel/`.
5. Back in Firebase: **Authentication → Settings → Authorized domains → Add domain** → `YOUR-ORG.github.io`.

## 3. Set up each iPad

1. Open the site address in **Safari**.
2. Tap **Share → Add to Home Screen → Add**.
3. Open **KWK Prizes** from the Home Screen (not from Safari).
4. Sign in once with the booth account. After that it stays signed in and syncs.
5. Settings → Accessibility → **Guided Access** on, and Display & Brightness → **Auto-Lock: Never**.

## Before the iPads go back to the warehouse

In the game: gear → PIN → **Sign out** (tap twice). That signs the iPad out and wipes the booth data from it.
Then delete the **KWK Prizes** icon from the Home Screen.

## Notes

- A brand-new iPad starts from the prizes in `seed.js` (copied from the claude.ai version). Once signed in, the live settings in Firebase take over.
- Uploaded prize images are stored as small copies inside the settings. The built-in KWK icons need no upload.
- If Wi-Fi drops, the game keeps working and syncs when it's back.
- Firebase's free Spark plan is far more than a booth needs.
