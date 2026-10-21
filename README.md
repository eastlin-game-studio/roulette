# American Roulette: website version

This is the same game as the claude.ai page. Its online table runs on Firebase instead of claude.ai accounts, so friends only need the link.

## One-time setup (about 20 minutes)

### 1. Firebase (the live table)
1. Go to https://console.firebase.google.com and click **Create a project**. Analytics can be off.
2. Open **Build → Authentication → Get started → Sign-in method**. Turn **Anonymous** on.
3. Open **Build → Realtime Database → Create database**. Pick a US location and choose **Start in locked mode**.
4. On the **Rules** tab, paste everything from `database.rules.json` and click **Publish**.
5. Click the gear → **Project settings → Your apps → Web (</>)**. Register an app named "roulette"; you don't need Firebase Hosting.
6. Copy the `firebaseConfig` object it shows. Make sure it has a `databaseURL`. If it doesn't, copy that URL from the top of the Realtime Database page.

### 2. Put the config in the game
Open `index.html` and search for `const FIREBASE_CONFIG=null;`. Replace `null` with the config object:

```js
const FIREBASE_CONFIG={apiKey:"…",authDomain:"…",databaseURL:"https://…firebaseio.com",projectId:"…",appId:"…"};
```

The API key is meant to be public. The database rules are what protect the table.

### 3. GitHub Pages (the website)
1. Create a new **public** repository on GitHub, for example `roulette`.
2. Upload `index.html` and `.nojekyll`. `README.md` is optional. Don't upload anything with passwords in it.
3. Go to **Settings → Pages → Build and deployment**, choose **Deploy from a branch**, then **main** and **/ (root)**, and click Save.
4. After a minute or two the site is live at `https://<your-username>.github.io/roulette/`.
5. In Firebase, go to **Authentication → Settings → Authorized domains** and add `<your-username>.github.io`.

## Playing
- **Host:** buy in, then click **Friends → Start a table**. Pick a seat; you're hosting. Click **Copy invite link** and send it.
- **Friends:** open the link and buy in. The table opens and they pick a seat.
- **Host controls:** click a player's card to **Make host** or **Remove from table**. The lobby also sets the table minimum and the spin timer for everyone.
- **Chat and reactions:** on a computer they're under Last numbers. On a phone, use the 💬 Chat button above the chips. Big wins post to the chat on their own.
- **The host's device runs the wheel,** so keep that tab open. If the host leaves, anyone seated can take over after about 20 seconds.

## Good to know
- It's play money, and chips are on the honor system: each device keeps its own bankroll.
- Anyone with the invite link or code can join. Only the host can spin, change settings, or remove players.
- Short strategy codes made on the website only work on the website. Backup codes (`RR2-…`) work everywhere.
- The free Firebase plan covers this use with plenty of room. Old tables stay in the database; you can delete `rooms` from the Realtime Database page anytime.
