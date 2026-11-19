# The Hidden Build — Skills Bank team game

Single-file HTML game (`index.html`). Teams of one **Messenger** (sees the secret brick blueprint) and **Builders** (each builds one part, never sees it). Parts are assembled and compared with the blueprint. Bilingual EN/AR, sounds + procedural music, live trainer console.

## Publish (GitHub Pages)
1. Create a repo, upload `index.html` and `.nojekyll` to the root.
2. Settings → Pages → Deploy from branch → `main` / root.
3. Open the published URL (do **not** use a preview/artifact viewer: it blocks the network).

## Run a session
1. Open the page → **Trainer Dashboard** → PIN `2026` (hides the UI only, not real security).
2. Share the player link (or just the 5-character room code). Each player types **name + room code + picks a team colour** on one screen (one colour per breakout room works well). In every team the first person to tap "I'll be the Messenger" sees the blueprint and guides the team; everyone else is a Builder.
3. Check the ready row, pick the blueprint (or Random), the time and **Messenger pin** (Off by default), press **START ROUND**.
4. After the round: **Reveal leaderboard**, projector view, CSV export.

## How bricks are split
The Messenger never builds. The 9 columns are divided between the Builders only (1 Builder: whole board, 2: 5+4, 3: 3+3+3, 4: 3+2+2+2, 5: 2+2+2+2+1). Players can switch team in the waiting room before the round starts.

## Chat is optional
Online trainings usually use breakout rooms, so the Messenger can simply talk. The in-game team chat is collapsed by default ("Team chat (optional)", with a new-message counter). The "picture named" keyword check and transcripts only exist for teams that used it; otherwise they show "—".

## Exit, pin, projector
- **⏏ EXIT** (top right, tap twice): leaves the game. In the lobby the player disappears from the team; during a round the team keeps waiting for that Builder's lock (or the timer).
- **Messenger pin** (trainer option, default Off): when On, the peek screen shows a "Pin it to my screen" button and the blueprint stays small on the Messenger's screen until unpinned. Off keeps the original "memory only" rule.
- **Projector view:** during the round each team gets a live progress bar (% of blueprint bricks placed, locks). The **SHOW BUILDS** button (top left) adds each team's current drawing (updates every ~10 s). After the round it shows the blueprint and the teams' builds, scores after Reveal.

## Scoring
Accuracy = correct bricks / (blueprint bricks + stray bricks), as %. Team score = accuracy × 10 + time bonus (0–100, only if every builder locked early AND accuracy ≥ 50%). Max < 1100. Everyone on the team gets the team score.

## How it works / honest limits
- Live sync uses the public **ntfy.sh** relay (SSE + POST). No backend, no keys. Public and not confidential: use fictional play only. `?relay=https://your-ntfy` uses your own server.
- The clock uses the relay's server time, so devices with wrong clocks stay in sync (±1 s).
- 4 teams, max 6 people per team (1 Messenger + up to 5 Builders). A team needs a Messenger and at least one Builder. No solo mode.
- "Picture named" is a keyword check on the Messenger's chat, not a quality judgement. Style chips are a self-pick, not an assessment.
- Free ntfy.sh may rate-limit or cap messages and ~30 streams per IP. Not measured: test before a large class.
- Tested headless (Playwright + mock relay): full team round, scoring, peek, chat, time-up, resume, Arabic, storage blocked. **Not tested:** real ntfy.sh, real phones/two devices, audio by ear, SSE-blocked polling for this game.

## Two-device checklist
1. Trainer on laptop, 2 phones as Messenger and Builder (same team).
2. Roster appears on both; the trainer's ready row turns green.
3. Start: countdown, timers match; Builder paints, Messenger peeks and chats.
4. Lock → reveal animation, score equals the trainer's team card.
