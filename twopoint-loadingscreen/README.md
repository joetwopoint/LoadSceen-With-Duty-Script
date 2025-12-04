# twopoint-loadingscreen

**REQUIRED TO WORK:**
- You must have at least **one valid TikTok or YouTube URL** configured in `html/script.js`.
- The resource folder must be named **`twopoint-loadingscreen`** and referenced with `ensure twopoint-loadingscreen` in your `server.cfg`.
- `html/logo.png` must exist (replace this file with your own logo image).

---

## What this loading screen does

- Shows a **phone-style frame** on the right with a video playing inside.
- Plays **random TikTok and/or YouTube Shorts** links you configure.
- Rotates a list of **server tips** on the left.
- Optionally shows a **staff list** with round character images (if you enable it).

Everything is controlled from plain HTML/CSS/JS files in the `html` folder.

---

## 1. Installation

1. Drop the folder into your server resources:

   ```text
   resources/[loadscreen]/twopoint-loadingscreen
   ```

2. In your `server.cfg`:

   ```cfg
   ensure twopoint-loadingscreen
   ```

3. Replace `html/logo.png` with your own server logo (keep the same name and location).

Players will see this while connecting to your server.

---

## 2. Main files

- `fxmanifest.lua`  
  - Tells FiveM this is a loadscreen resource and points to `html/index.html`.

- `html/index.html`  
  - The main layout (left panel text, right panel phone frame, stats/tips blocks).

- `html/style.css`  
  - All styling: background, phone frame look, text alignment, etc.

- `html/script.js`  
  - All logic and **config options**: shorts list, staff list, timing, etc.

- `html/staff/`  
  - Optional staff avatar images (round portraits) if you enable the staff list.

---

## 3. Things you can customize

Open `html/script.js` – at the top you’ll see the main config block.

### 3.1 Staff list (middle column)

```js
const STAFF_ENABLED = false;

const staffMembers = [
  // {
  //   name: "Jane Doe",
  //   role: "Community Manager",
  //   description: "Handles support & questions.",
  //   image: "staff/jane.png"
  // }
];
```

- Set `STAFF_ENABLED` to `true` to show the staff column between the left panel and the phone.
- Add entries to `staffMembers`:
  - `name`: staff name shown in the card
  - `role`: small role/title line under the name
  - `description`: short text (optional)
  - `image`: path to an image in `html/staff/` (for example `staff/jane.png`)

Place your character portraits in `html/staff/` and use those file names in `image`.

---

### 3.2 TikTok / YouTube shorts

```js
// "tt"   -> TikTok only
// "yt"   -> YouTube only
// "both" -> TikTok + YouTube
const SHORT_SOURCE = "tt";

// TikTok links
const tikTokUrls = [
  "https://www.tiktok.com/@sunvalleyroleplay2/video/...",
  // add/remove your own TikTok URLs here
];

// YouTube links
const youTubeUrls = [
  // "https://www.youtube.com/shorts/VIDEOID",
  // "https://youtu.be/VIDEOID",
  // "https://www.youtube.com/watch?v=VIDEOID"
];
```

- `SHORT_SOURCE` controls **what type of clips** are used:
  - `"tt"` → only TikTok links in `tikTokUrls`
  - `"yt"` → only YouTube links in `youTubeUrls`
  - `"both"` → mix of both lists
- Replace the sample TikTok URLs with your own account’s videos if you want.
- Add your own YouTube Shorts or videos to `youTubeUrls` if you want to use YouTube.

> **Important:** Make sure there is **at least one link** in the active list or the frame will stay blank.

---

### 3.3 Clip duration (how often it switches)

```js
const CLIP_DURATION_MS = 30000; // 30 seconds
```

- This controls **how long** each clip shows before the script picks another one.
- Set to your preferred value (in milliseconds), e.g.:
  - `20000` = 20 seconds
  - `45000` = 45 seconds

---

### 3.4 Server tips on the left

```js
const tips = [
  "Be respectful to other players. RP > FRP.",
  "Read the rules in Discord before you hit the streets.",
  "Use push-to-talk and keep comms clear during scenes.",
  "Record your POV – it helps with reports and clips.",
  "Have fun, but remember: actions have consequences."
];
```

- Edit, remove, or add as many tip strings as you like.
- The script will rotate through them automatically every few seconds.

---

### 3.5 Volume behavior (YouTube only)

```js
let volumePercent = 20;
```

- This is a **logical volume** used only for YouTube embeds:
  - If `volumePercent` is `0`, the YouTube embed is muted.
  - If greater than `0`, the embed is unmuted.
- TikTok does **not** support volume control from this script; audio is controlled by the player and browser.

You can also remove any on-screen text about keyboard volume controls if you don’t want to mention them.

---

## 4. Changing visuals (phone frame, colors, fonts)

All visual styling is in `html/style.css`. Some useful sections:

- `.phone-frame`  
  - Phone border color, thickness, rounded corners, drop shadow.

- `.video-title`, `.controls-hint`, `.video-note`  
  - Text above and below the phone; aligned to match the phone width.

- `.background`, `.overlay`, `.background-logo`  
  - Background gradients, dark overlay, and big transparent logo behind everything.

Feel free to tweak colors, fonts, shadows, and layout here to match your server theme.

---

If you ever break something, you can restore the original `script.js`, `style.css`, or `index.html` from a fresh copy of this resource and re-apply your tweaks step by step.
