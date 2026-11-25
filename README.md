# Age of Crowns

A medieval strategy game of world conquest, built to be played on a phone. One HTML file, no install, no account.

**Play:** https://iqbalnabeel-cmd.github.io/age-of-crowns/

Add it to your home screen and it opens full screen with its own icon.

## What it is

Lead one of 8 historical empires across a real world map: 80 cities over 367 named stretches of
country, projected from actual coordinates. Hold 30 cities to win.

- **A clock, not turns.** The world runs in hours and keeps running while you are away.
- **18 units** across six arms and three tiers, with armour, wounds and scouting.
- **Five materials** plus manpower. Every city makes one of grain, timber, iron, stone or horses,
  chosen by what the place really was, and all eight crowns trade them on an open market.
- **Rivers, roads and nine kinds of ground**, all of which change how far and how fast you march.
- **A navy** of three ships that can blockade and bombard, but never capture, because ships do
  not hold ground.
- **Multiplayer** on a Cloudflare Worker: a world code, one server clock, all 8 crowns.

## The files in here

| File | What it is |
| --- | --- |
| `index.html` | **The game.** This is the one that is live at the link above. Uploading over it ships a new build to everyone, including anyone who has it on their home screen. |
| `worker.js` | The multiplayer server. Cloudflare deploys it from this repo automatically. |
| `aoc-source-v*.zip` | The full source tree for each build, plus the built file. This is the project's backup. |
| `aoc-v*.html` | Older builds, kept so an old link still works. Not needed to play. |

The game is built from a source tree of separate files and concatenated into the single
`index.html`. `node build.mjs --verify` proves the tree rebuilds the shipped file byte for byte,
which is how the project has been recovered three times after losing its build environment.

Built by Nabeel with Claude.
