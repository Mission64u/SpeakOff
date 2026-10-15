# Speak Off: Impromptu Challenge

A live, multi-team impromptu speaking game for club events. Teams submit topics in secret, the host draws a random topic from another team's pool, a speaker has a timed turn, and the room rates the speech. Scores, topics, and ratings update live on every device. Players need no account and no login. They just open the link.

**Live game:** https://mission64u.github.io/SpeakOff/

---

## Quick start (host)

1. Open the game link. Under the title, look for **Live · room: main**. That means it is connected.
2. Click **Host Mode** and set a PIN. You can now add, rename, and remove teams (2 to 6) and enter each team's rep name.
3. Type the **Timer** and **Grammarian** names in the roles bar.
4. Send players your event link (see [Rooms](#rooms)). Everyone must use the exact same link.
5. Let teams submit topics, then start the first round.

## How a round works

1. **Draw Topic.** The stage shows which team is up next. The host draws a random topic written by a *different* team.
2. **Timer.** Choose 30s, 60s, 90s, or 2m, then start the timer when the speaker begins. The clock turns gold at 15 seconds and red at 5. The timer is shared, so everyone sees the same clock.
3. **Grammarian notes.** The Grammarian types notes and saves them. Notes collect in the Grammarian's Report across the whole event and are never cleared between rounds.
4. **Rate the speech.** Everyone except the speaker rates five criteria from 1 to 5 and submits once per speaker: Content & Message, Organization, Vocal Variety & Delivery, Body Language & Confidence, and Overall Impact. Averages update live.
5. **Score.** The host reviews the averages and either taps **Apply to Scoreboard** for the suggested points or uses the +1, +3, +5, and −1 buttons.
6. **Next Turn.** The used topic is retired and the next team is up.

## For players

- Find your team's card near the bottom of the page.
- Type a topic (150 characters max) and tap **Add Topic**. Only a running count is shown. Topics stay hidden until one is drawn.
- When a speaker is up, rate them on the five criteria and tap **Submit My Rating**.

## Present Mode

Click **Present Mode** to hide setup panels, the roles bar, the evaluation panel, the Grammarian's Report, and the topic boxes, for a clean projector or screen-share view. It affects only the device you click it on.

## Rooms

A room is a separate game with its own teams, scores, topics, ratings, and notes. Choose a room by adding `?room=` and a name to the end of the link:

| Link | Room |
|---|---|
| `https://mission64u.github.io/SpeakOff/` | `main` (default, good for practice) |
| `https://mission64u.github.io/SpeakOff/?room=november` | `november` |

- Rooms are created automatically the first time someone opens the link. No setup is needed in GitHub or Firebase.
- Use letters, numbers, hyphens, and underscores (up to 40 characters). Capitalization counts, so lowercase is safest.
- Each room sets its own Host PIN the first time Host Mode is used.
- To run a fresh game, use a new room name instead of reusing an old one.

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

**Clearing old games:** Old rooms stay in the database. They are harmless, but you can delete them in Firebase under **Firestore Database → Data → rooms**.

## Troubleshooting

| What you see | What to try |
|---|---|
| Yellow line: "Not connected yet" | The Firebase settings are missing or didn't load. Check the `FIREBASE_CONFIG` block in `index.html`. |
| Red line: "Connection problem" | Check the Firestore rules and the expiry date. Confirm the `apiKey` was copied exactly. |
| 404 page | Wait a couple of minutes. Confirm the file is named `index.html` and the repository is Public. |
| Add Team box missing | Turn on Host Mode. Team editing is locked until then. |
| Players see an empty game | They may be in a different room. Make sure everyone uses the exact same link. |
| Changes not showing after an update | Refresh the page, or clear the browser cache. |
