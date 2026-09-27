# Roblox Game Project — Reference Notes

Working notes for the Roblox game we're building together. The final deliverable is a
prompt file you download and load into Claude Code in VS Code.

## Setup (as of 2026-09-27)

- **Builder:** Claude Code in VS Code, already connected to Roblox Studio (Studio's built-in MCP connector).
- **UI pipeline:** Figma → FrameWisp → Roblox Studio. There's no Figma design yet, so the prompt has to spell out every screen.
- **FrameWisp plan:** Free.
- **The game:** Different from both reference videos. Concept still to come.

## FrameWisp facts (from framewisp.com)

- **Workflow:** Select a Figma frame, press Export, then paste the 6-character code into the Studio plugin. Images upload to your own Roblox account.
- **Output:** Frame, TextLabel, TextButton, ScrollingFrame and CanvasGroup, with UIStroke, UICorner and UIGradient attached. Sizes and positions use Scale, plus UIAspectRatioConstraint.
- **Free tier:** 5 conversions a day, up to 15 images each. It covers layout, text, colours, strokes, scrolls and grids.
- **Pro-only features:** motion, working buttons (`_button`, `_hover`, `_clicked`, `_tab:X`, `_open:X`, `_close`), live data labels (`{Coins}`) and libraries.
  - **On Free, all button logic and animation must be written in Luau** (TweenService and similar).
- **Not supported:** blend modes, auto-layout, Figma constraints, backdrop blur.
  - Text with gradients or custom fonts gets baked into an image.
- **Re-importing** a frame never touches your scripts. Scripts should find UI by name, so re-exports don't break them.

## Video 1 — "My Roblox Game Makes $12,535/mo (3K CCU)" by MoseyTube77
https://youtu.be/a170E9klbP4

**Game:** *Guess the Job or Die.* One player picks a secret job and the other guesses it letter by letter. A right guess wins cash; a wrong guess kills you.

**Stats:** peaked at 3K concurrent players, averages about 2K, 2.1M visits in about a month, and made 358,166 Robux in 72 hours.

**The formula:** A simple core loop anyone can understand in 10 seconds, with no tutorial needed. Then stack systems on top of it that give players reasons to stay, come back and spend.

- **Collection:** chairs and limited skins, plus a daily rotating shop.
- **Come-back systems:** daily rewards, playtime rewards, group rewards and VIP daily rewards.
- **Streaks:** tracked on the leaderstats, and you can pay Robux to restore a broken streak. Losing progress hurts, so people pay.
- **A "clippable" chaos mechanic:** stealing cash from other players. It creates drama that YouTubers and clippers pick up.

**Monetization:**
- Game passes:
  - VIP: 1.5× cash, VIP chat and cosmetics.
  - 2× cash, 2× wins and 2× streak.
- Developer products: cash packs, win packs, and hints ("reveal job", "reveal one letter").
- Cosmetics across many price points.

**How it was built:** Claude for the systems, the creator's own dev skills, and a hired UI polisher. The lesson is to outsource only your bottleneck.

## Video 2 — "I Tried Making a Viral Roblox Game With AI" by LanceyPoo
https://youtu.be/xxeNaxrfRVs

**Stack:** Claude Code connected to Studio's built-in MCP. Claude Design generated the 3D models as GLB files, which were imported into Studio. ChatGPT made the icons and images.

**Game:** *My Duck Pond / My Duck Empire*, inspired by *My Fish Empire*. The loop:
1. Ducks in your pond drop bread.
2. The bread rides a conveyor to a collection pad, and you collect it in a basket.
3. You sell it at the bakery for cash.
4. Cash buys eggs, which hatch into ducks of different rarities.
5. You place ducks in a limited number of nest slots.
6. You upgrade ducks up to level 10, or merge two into a bigger one with bigger output.
7. You buy more nests, and eventually rebirth.

**Extras:**
- Index and leaderboards: time played, biggest flock, richest farmer.
- Daily gifts, codes, and a weather machine that gives 2× boosts.
- Merchant and bakery upgrades, such as a bread magnet.
- Sprint, and holding a duck in your hand.

**UI and polish details:**
- Billboard GUIs appear only when you're close.
- A big floating player name sits above each plot.
- Notifications fade out instead of lingering.
- Bread is a physical object.
- Duck variants are procedural: one base mesh with different materials, colours, accessories and VFX.

**Workflow that worked:**
- Build a tiny test version first, then iterate.
- Send reference screenshots for the art style (low-poly), and highlight problem areas in screenshots.
- Batch fixes into one "mega prompt" per round of play-testing.
- Have Claude write the step-by-step plan first, then feed it the steps one at a time.
- Keep producing other assets while Claude works.

**What went wrong (avoid these):**
- The sound effects were too loud.
- Mobile layout was broken.
- The economy was too easy, so the game could be speed-run.
- The UI took up too much of the screen.
- **The new-player funnel failed.** Right after the tutorial, players couldn't afford their next egg, so they left.
- Ads: $6.24 bought about 83K impressions, but click-through was poor and no players were retained.
  - **Lesson:** the first 2–5 minutes and the thumbnail decide everything.

## Market research — Roblox Top Playing and Top Trending (screenshots, 2026-09-27)

**Dominant genre: simulators, meaning "number goes up" games.** You grind a stat, collect or hatch things, upgrade, and repeat.

The hottest simulator formats right now:
- **"Steal a ___"** (steal-and-defend bases): Steal An Egg is #1 overall with 1.2M players. Also Steal a Brainrot, Steal A Verity, Steal From The Rich and Don't Steal the Bobo.
- **"+1 ___ every second"** incremental games: about 12 titles, including +1 Speed Keyboard Escape, +1 Loot To Forge, +1 Tongue Escape, +1 Wings/Strength For Eggs, +1 Mog Evolution and +1 Jump Keyboard Tower.
- **"___ for Eggs"** (a hatching reward loop): Race for Eggs, Swing For Eggs, Wings For Eggs and Strength For Eggs.
- **Build, grow and tycoon games:** Grow a Garden, Build the Pyramid, Build a Boat, Drill to Earth's Core, Sell Lemons and Restaurant Tycoon 3.

The other big groups:
- **Horror and survival:** 99 Nights, Forsaken, DOORS, Piggy, Dandy's World, and "Anomaly" games.
- **Roleplay:** Brookhaven, Berry Avenue, Bloxburg, Dubai RP.
- **PvP and FPS:** RIVALS, MM2, Blade Ball, Knife Duels.
- **Anime fighting:** Blox Fruits, Slayers 2, Strongest Battlegrounds, Anime Dice.
- **Soccer is a rising niche:** Blue Lock Rivals, Illegal Soccer, Realistic Street Soccer, Freekick Challenge and Blue Lock Farm (98% liked, 11.8K players), which you flagged.

**Thumbnail patterns:** bright, saturated colours; one big character or face; floating "+1" numbers; huge money counters; NEW or UPDATE badges.

## Game concept v3 (your decisions from 2026-09-27)

**Name:** to be decided later. The working title is "+1 Speed Egg Heist".

**Decided:**
- **+1 Speed per click.**
- **Seven eggs, each in its own zone.**
- **A zone's monster chases you home after you grab its egg.**
- **Eggs hatch in your base** into a random pet from that egg's own list.
- **Only pets in a base slot earn coins.** Extra pets wait in your inventory.
- **Hatched pets can't be stolen.** Only incubating eggs can.
- **Stealing is free once every 5 minutes**, and Robux "Steal Now" skips the wait.
- **When someone steals from you, only you (the owner) chase them.**
- **Pets keep earning offline**, capped at 8 hours.

**Bases (2 floors):**
- Floor 1 has one doorway with a laser door, plus a button inside to close it.
  - The door stays closed for 15 seconds, then there's a 5-second cooldown before it can close again.
- Floor 2 is reached by an outside staircase on the side of the base. It has its own laser door with the same 15-second / 5-second rules.
- **Proposed:** the laser door buttons are physical, inside the base, and only the owner can use them. To guard your base you have to stay home.
- **Proposed:** you start with Floor 1 (2 incubators, 6 pet slots). Floor 2 is bought with coins and adds 2 incubators and 8 pet slots.

**Zones:**

| # | Zone | Egg | Monster | Hatch time | Speed to enter (proposed) |
|---|---|---|---|---|---|
| 1 | Meadow | Grass Egg | Angry Chicken | 30 seconds | 0 |
| 2 | Forest | Leaf Egg | Bear | 1.5 minutes | 100 |
| 3 | Desert | Sand Egg | Giant Scorpion | 3 minutes | 500 |
| 4 | Snow | Ice Egg | Yeti | 10 minutes | 2,000 |
| 5 | Volcano | Lava Egg | Lava Golem | 15 minutes | 8,000 |
| 6 | Crystal Cave | Crystal Egg | Crystal Spider | 30 minutes | 30,000 |
| 7 | Void | Galaxy Egg | Shadow Beast | 45 minutes | 100,000 |

**Pets** (chance of hatching, and coins per second while in a base slot):

- **Grass Egg:** Chick (Common, 55%, 1/s), Bunny (Uncommon, 28%, 3/s), Ladybug (Rare, 12%, 6/s), Hedgehog (Epic, 4.5%, 12/s), Golden Duck (Legendary, 0.5%, 30/s)
- **Leaf Egg:** Squirrel (Common, 55%, 5/s), Fox (Uncommon, 28%, 12/s), Owl (Rare, 12%, 25/s), Deer (Epic, 4.5%, 60/s), Forest Spirit (Legendary, 0.5%, 150/s)
- **Sand Egg:** Lizard (Common, 55%, 25/s), Camel (Uncommon, 28%, 60/s), Fennec Fox (Rare, 12%, 130/s), Sand Serpent (Epic, 4.5%, 300/s), Pharaoh Cat (Legendary, 0.5%, 750/s)
- **Ice Egg:** Penguin (Common, 55%, 150/s), Seal (Uncommon, 28%, 350/s), Polar Bear (Rare, 12%, 800/s), Snow Leopard (Epic, 4.5%, 1,800/s), Frost Dragon (Legendary, 0.5%, 4,500/s)
- **Lava Egg:** Magma Slime (Common, 50%, 800/s), Fire Salamander (Uncommon, 30%, 1,800/s), Lava Hound (Rare, 14%, 4,000/s), Phoenix (Epic, 5%, 9,000/s), Inferno Dragon (Legendary, 0.9%, 22,000/s), Volcano King (Mythic, 0.1%, 60,000/s)
- **Crystal Egg:** Gem Beetle (Common, 50%, 4,000/s), Crystal Bat (Uncommon, 30%, 9,000/s), Diamond Turtle (Rare, 14%, 20,000/s), Amethyst Wolf (Epic, 5%, 45,000/s), Prism Unicorn (Legendary, 0.9%, 110,000/s), Crystal Queen (Mythic, 0.1%, 300,000/s)
- **Galaxy Egg:** Star Blob (Common, 50%, 20,000/s), Moon Cat (Uncommon, 30%, 45,000/s), Comet Fox (Rare, 14%, 100,000/s), Nebula Jellyfish (Epic, 5%, 225,000/s), Black Hole Dragon (Legendary, 0.9%, 550,000/s), Cosmic Overlord (Mythic, 0.09%, 1,500,000/s), Void Emperor (**SECRET**, 0.01%, 5,000,000/s, announced to the whole server when it hatches)

**Order for the build prompt (only after your OK):**
1. Map
2. Bases
3. Clicking for speed, plus saving
4. Eggs and monsters
5. Hatching, pets and coins (including offline earnings)
6. Stealing
7. Shop and rebirth
8. UI and animation
9. Daily rewards, streaks and the Index
10. Robux items
11. Polish and mobile

After each step, Claude stops so you can play-test.

## Instagram creators (not yet reviewed)

- **smartcode_academy_official:** a Ukrainian online programming school, so not all of its posts are about Roblox.
- **shadundercover:** goes by "shadarchives", about 1,251 followers.
- Instagram is blocked from the cloud container. We need a Firecrawl connection (through Composio) or reel links to review them.

## Open questions

- What is your game concept?
- Which Instagram reels matter most?
