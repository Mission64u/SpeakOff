# Speak Off: Impromptu Challenge

A live, multi-team impromptu speaking game for club events. Teams submit topics in secret, the host draws a random topic from another team's pool, a speaker has a timed turn, and the room rates the speech. Scores, topics, and ratings update live on every device. Players need no account and no login. They just open the link.

**Live game:** https://mission64u.github.io/SpeakOff/

---

## Quick start (host)

1. Open https://mission64u.github.io/SpeakOff/ and tap **Start a New Game**. This creates a game with a random six-character code.
2. Under the title, look for **Live · game: YOURCODE**. That means it is connected.
3. Click **Host Mode** and set a PIN. You can now add, rename, and remove teams (2 to 6) and enter each team's rep name. The **Invite players** box also appears (see [Game codes and QR](#game-codes-and-qr)).
4. Type the **Timer** and **Grammarian** names in the roles bar.
5. Share the QR code, join link, or game code with your players.
6. Let teams submit topics, then start the first round.

## How a round works

1. **Draw Topic.** The stage shows which team is up next. The host draws a random topic written by a *different* team.
2. **Timer.** Choose 30s, 60s, 90s, or 2m, then start the timer when the speaker begins. The clock turns gold at 15 seconds and red at 5. The timer is shared, so everyone sees the same clock.
3. **Grammarian notes.** The Grammarian types notes and saves them. Notes collect in the Grammarian's Report across the whole event and are never cleared between rounds.
4. **Rate the speech.** Everyone except the speaker rates five criteria from 1 to 5 and submits once per speaker: Content & Message, Organization, Vocal Variety & Delivery, Body Language & Confidence, and Overall Impact. Averages update live.
5. **Score.** The host reviews the averages and either taps **Apply to Scoreboard** for the suggested points or uses the +1, +3, +5, and −1 buttons.
6. **Next Turn.** The used topic is retired and the next team is up.

## For players

- Scan the host's QR code or tap the join link. Or open https://mission64u.github.io/SpeakOff/ and type the game code.
- Find your team's card near the bottom of the page.
- Type a topic (150 characters max) and tap **Add Topic**. Only a running count is shown. Topics stay hidden until one is drawn.
- When a speaker is up, rate them on the five criteria and tap **Submit My Rating**.

## Present Mode

Click **Present Mode** to hide setup panels, the roles bar, the evaluation panel, the Grammarian's Report, and the topic boxes, for a clean projector or screen-share view. It affects only the device you click it on.

## Game codes and QR

Every game is separate, with its own teams, scores, topics, ratings, and notes. Each game is identified by a random six-character code.

- **Start a game:** On the main page, tap **Start a New Game**. Or, in Host Mode, tap **New Game Code** in the Invite players box.
- **Invite players:** The Invite players box (visible to the host after Host Mode is on) shows the game code, a QR code, and the join link, with Copy buttons. It also shows in Present Mode, so you can project it.
- **Join a game:** Players scan the QR code or tap the link. Or they open the main page and type the code on the join screen.
- **Different clubs:** Each club can run its own game with its own code, or several clubs can play as teams in one game (up to six teams).
- **Fresh game:** Use a new code. Old games stay in the database and are harmless.
- **Code rules:** Codes are not case-sensitive. A link ending in `?room=` followed by a code (for example `?room=k7m2q9`) opens that game directly. Letters, numbers, hyphens, and underscores only, up to 40 characters.
- **Keep it private:** A game code works like a password. Anyone who has the code or link can join, so share it only with your players.
- Each game sets its own Host PIN the first time Host Mode is used.

## Good to know

- **Host controls are not locked.** Only team names and rep names are protected by the Host PIN. Draw Topic, the timer, Next Turn, and the score buttons work on every device, so ask players to leave them to the host.
- **Ratings are not limited per person.** The game does not stop someone from rating more than once, so rely on the honor system.
- **Topics are hidden on screen, not encrypted.** Someone with technical skill could view them through browser developer tools. The game is built for friendly club use, not private data.
- **The Host PIN is a simple lock,** not strong security. Don't reuse a password you use anywhere else.

## How it is built

- One file, `index.html`, hosted free on GitHub Pages.
- Live data is stored in a Firebase Firestore database (free Spark plan).
- No accounts, sign-in, or payment are needed for players or the host.

## Maintenance

**Firestore rules expire on December 31, 2026.** After that date the game stops saving data. To extend it:

1. Go to the Firebase console, open the SpeakOff project, then **Firestore Database → Rules**.
2. Change the date in the line `request.time < timestamp.date(2026, 12, 31)` to a later date.
3. Click **Publish**.

**Updating the game:**

1. Edit `index.html` and keep your Firebase settings in the `FIREBASE_CONFIG` block near the top of the script.
2. In this repository, choose **Add file → Upload files**, upload the new `index.html` (the same name replaces the old one), and click **Commit changes**.
3. Wait a minute or two, then refresh the game link.

**Clearing old games:** Old games stay in the database. They are harmless, but you can delete them in Firebase under **Firestore Database → Data → rooms**.

## Troubleshooting

| What you see | What to try |
|---|---|
| Yellow line: "Not connected yet" | The Firebase settings are missing or didn't load. Check the `FIREBASE_CONFIG` block in `index.html`. |
| Red line: "Connection problem" | Check the Firestore rules and the expiry date. Confirm the `apiKey` was copied exactly. |
| 404 page | Wait a couple of minutes. Confirm the file is named `index.html` and the repository is Public. |
| Add Team box or Invite players box missing | Turn on Host Mode. Both are hidden until then. |
| Players see an empty game | They may be in a different game. Make sure everyone uses the same code or QR. |
| Join screen says to enter a code | The link was missing the game code. Scan the QR code again, or type the code. |
| QR code shows "QR unavailable" | The QR tool couldn't load. Use the join link or game code instead, or paste the link into any free QR generator. |
| Changes not showing after an update | Refresh the page, or clear the browser cache. |
