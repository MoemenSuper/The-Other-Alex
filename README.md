# Alex Horror Mod — Command Event Guide

Use this guide to test events, film scenes, and surprise friends on a multiplayer server.

> **Important:** almost every command in this guide is an **operator/admin command** (permission level 2). Enable cheats in a single-player world, or give yourself operator status on a server. `/spawnalex` is the one public command.

## Before you start

### Triggering an event for someone else

Most event commands can target another online player. For example, to put Alex behind a player called `AlexFan`, run:

```mcfunction
/testbehindyou AlexFan
```

Without a player name, run the command as the target player.

### Why a forced event can fail

“Force” means “try now,” not “make it happen in an impossible place.” Some events still need the right setup. Common requirements are:

- A loaded, safe place to spawn an entity (solid ground, headroom, and often a position outside the player’s view).
- The correct setting: cave, bed, door, ladder/scaffolding, or Overworld, depending on the event.
- A living, non-spectator target; some events also reject Creative mode.
- Required content: a saved voice clip, chat history, an optional integration mod, a Herobrine entity, or a valid structure.

If Minecraft reports `NO_VALID_SPAWN`, clear space around the target and retry.

### Recommended filming setup

1. Use Survival or Adventure mode unless the event says otherwise.
2. Keep the target in a loaded area with room behind and around them.
3. For a reveal, have the player look away before running the command. Several events intentionally require an off-screen spawn.
4. For natural gameplay, leave Director silence off. For controlled takes, use `/alex director silent on` to stop other Director events interrupting the scene.
5. Run `/alex director silent off` when finished.

## The mod’s event language

The mod uses these terms:

| Term | Plain meaning |
| --- | --- |
| **Hint** | A subtle sign that Alex may be nearby. |
| **Pressure** | A stronger, paranoia-building scare. |
| **Manifestation** | A direct appearance or major reveal. |
| **Mimic** | A false player/doppelganger using a real player’s name, skin, or equipment. |
| **EventDirector** | The system that normally picks when events happen and stops them from repeating too obviously. |
| **Creator Showcase** | A setting that tries to show a player events they have not seen yet. |
| **Integration** | An optional event that reacts to another installed mod. |

Alex works best as slow-burn psychological horror. Use commands to test or film a scene, then leave space between major events.

### Experimental Creator Showcase mode

**Creator Showcase is experimental and disabled by default.** Enable it in the common config:

```toml
[creator_showcase]
enabled = true
```

It records the scheduled events each player has seen and prefers eligible unseen events. Seen events can still repeat. Leave `enabled = false` for normal event selection.

Creator Showcase keeps safety checks, cooldowns, and location requirements. It cannot start a cave event outside a suitable cave. The world saves each player's progress.

---

## Fast-start: reliable showcase events

| Goal | Command | What to do next |
| --- | --- | --- |
| Put an Alex behind the player | `/testbehindyou` | Walk forward, then turn around. |
| Put an unseen animal watcher nearby | `/teststaringcat` | Look around slowly. |
| Create a sign | `/testsign look_behind` | Read the sign; follow its instruction. |
| Set up a sleep reveal | `/testsheswatching 10` | Get into bed within 10 seconds. |
| Send the player into the sky | `/skyteleport` | Let the fall play out; it is designed to return them safely. |
| Start the Moog City sequence | `/alex moogcity trigger` | Let the timed music and visual cues run uninterrupted. |

---

## Direct player scares

| Command | What it does | Requirements and useful details |
| --- | --- | --- |
| `/testbehindyou [player]` | Spawns Alex behind the target for a turn-around reveal. | Needs a valid grounded spawn with headroom behind the player. `/resetbehindchance` resets this event family’s natural chance for the command runner. |
| `/testrightbehindyou [player]` | Triggers the more immediate “right behind you” version. | Give the target space behind them and keep their camera facing away from it. |
| `/testlightning [player]` | Forces Alex’s lightning-strike scare. | Needs the controller’s valid world/target conditions. Best outdoors with an open sky for a readable shot. |
| `/testbolt [player]` | Arms a turn-around Alex test, rather than spawning her immediately. | After running it, turn roughly 110° or more from the current facing direction. The command prints the starting yaw. |
| `/testclimbbolt [player]` | Arms an Alex reveal during a climb transition. | Use a ladder or scaffolding route that leads to a new landing. Check `/testclimbbolt status`; cancel with `/testclimbbolt cancel [player]`. It rejects dead, spectator, and Creative targets. |
| `/testnecksnap [player]` | Triggers the Neck Snap scare. | Requires the controller to find a valid target/setup. Use a normal survival-style play space. |
| `/testinvisiblepush [player]` | Forces an unseen shove. | Give the player safe room in the direction they may move; do not stage it next to fatal drops. |
| `/testfootstepsbehind [player]` | Plays the footsteps-behind pressure event. | The player should be moving through a quiet area; headphones make the effect clearer. |
| `/testtheyarewatching [player]` | Tier-2 “They’re All Watching”: nearby vanilla entities begin tracking nearest players. | Nearby mobs make the change visible. |
| `/testtheyarewatching tier3 [player]` | Tier-3 version of the same watching event. | Use a populated but safe area so the coordinated attention reads on camera. |
| `/testsheswatching [wait_seconds] [player]` | Arms a sleep-triggered Alex scene; default wait is 180 seconds, allowed range is 10–600. | The target must be alive, not spectator, then start sleeping before the timer expires. The bed needs a loaded, visible, safe nearby spawn position. |
| `/skyteleport [player]` | Starts the sky-fall scare. | **Overworld only**; a player already in this event cannot start it again. `/skyteleport cancel [player]` returns them to safety; `/skyteleport stats` shows active falls. |

## Cave and mining events

Caves are intentionally a first-class Alex setting. Build a real cave/tunnel rather than a brightly lit box: several events need cave geometry or a concealed spawn anchor.

| Command | What it does | Requirements and useful details |
| --- | --- | --- |
| `/testghostmining [player]` | Creates ghost-mining activity. | Adapts its presentation for tunnels versus open caves. A cave/mining setting gives the strongest result. |
| `/testmirroredmining [player]` | Arms mirrored mining for two seconds. | Start mining immediately after the command. |
| `/testcavefind [player]` | Spawns Cave Find Alex at a suitable nearby anchor. | The target must be alive and the controller must find a valid spawn. Use an actual cave with room for an entity. |
| `/testcavecry start [player]` | Starts the multi-phase Cave Crying scene. | **Overworld, alive player, in a cave, and a valid cave anchor** are required. It is deliberately not a generic sound effect. |
| `/testcavecry status [player]` | Shows the Cave Crying scene state and diagnostics. | Run this after a refusal to see the active/setup state. |
| `/testcavecry stop [player]` | Stops an active Cave Crying scene. | Only works while that player has an active cave-cry scene. |

## Watching entities and Mimics

| Command | What it does | Requirements and useful details |
| --- | --- | --- |
| `/teststaring [player]` | Spawns either a staring chicken or white-eyed cat. | Finds a valid position outside the target’s field of view. Look away first and give it reachable ground. |
| `/teststaringcat [player]` | Spawns the white-eyed cat version. | Same off-screen safe-spawn requirement. |
| `/teststaringchicken [player]` | Spawns the staring chicken version. | Same off-screen safe-spawn requirement. |
| `/testfakeplayer [player]` | Spawns a Fake Player Mimic. | Requires saved player data to mimic and a valid nearby spawn. On a fresh world/server, let players join and play first so there is identity data to borrow. |
| `/teststalker [player]` | Spawns a hiding Fake Player Stalker. | Needs a suitable nearby cover/spawn location. Let the target explore instead of looking directly at the spawn point. |
| `/testherobrecow [player]` | Places a Herobrine Cow in a nearby cow farm. | Requires a valid nearby cow-farm setup. Build the farm before filming. |
| `/testhauntedgolem [player]` | Spawns a haunted iron golem. | Needs a valid spawn location near the target. Use a village or open base area for context. |

## Bases, doors, signs, and world changes

| Command | What it does | Requirements and useful details |
| --- | --- | --- |
| `/testdoorknock [player]` | Starts the door-knocking sequence. | Requires a valid door and works best at a small house.<br>1. Hear the knock; go outside to check.<br>2. Go back inside and close the door; a few seconds later, pounding starts.<br>3. On the third return, open the door and check outside. Return inside and turn around: if other players are inside, you see their doppelgangers, but they cannot see them.<br>`/resetdoorchance` resets the natural door-knock chance. |
| `/testabandonedbase [player]` | Haunts the area around the player with soul fire, a “LEAVE NOW” sign, and player skulls. | This edits the world around the target. Use a backed-up test base or a disposable recording world. The debug command can be run repeatedly. |
| `/testmassivenull [player]` | Starts the Massive Null scene. | After starting it, keep walking and then turn around. Use `/testmassivenull status [player]` to inspect it and `/testmassivenull stop [player]` to end it. |
| `/testsign <type> [player]` | Spawns one selected Alex sign behind the target. | Needs a valid sign placement. Look away and leave a block surface/space behind the target. Types are listed below. |

### Sign types

| Type | Intended message/feature |
| --- | --- |
| `chat_quote` | Quotes one of the player’s saved chat messages. Chat history is required. |
| `chat_response` | Simulates Alex listening and replying to chat; the command bypasses only the normal cooldown. It may need chat history and uses the live listening policy. |
| `fourth_wall` | A “this is not a game” style message. |
| `watching` | Personal “I can see you” message. |
| `identity` | Identity-crisis wording using the player’s name. |
| `turn_around` | Tells the player to turn around. |
| `look_behind` | Asks the player to look behind; staring at it can create a follow-up. |
| `death` | Fake-death message. |
| `help` | Help-request message. |
| `location` | References the player’s coordinates. |
| `cave` | Predictive cave warning. |
| `crafting` | Comments on crafting. |
| `inventory` | References the player’s items. |

Use `/testsign` with no type to print the in-game sign command help. `/chatinfo [player]` shows how much chat is stored; `/clearchathistory` clears the runner’s history.

## Alex sightings, music, rain, and Director tests

| Command | What it does | Requirements and useful details |
| --- | --- | --- |
| `/alexspot trigger [player]` | Forces a random standalone Alex sighting. | Needs a valid scene/spawn. |
| `/alexspot trigger creeping\|stalking\|lurking [player]` | Forces that specific sighting style. | Use the named style for repeatable takes; keeping the target unaware of the spawn makes it read best. |
| `/alexspot enabled on\|off` | Enables or disables autonomous standalone sightings. | Persists as the controller’s runtime setting. |
| `/alexspot rarity common\|uncommon\|rare` | Sets natural sighting frequency. | Use `rare` for normal horror pacing; `common` is useful only for testing. `/alexspot status` shows day/night chances. |
| `/alex moogcity trigger [player]` | Starts the timed Moog City Event. | This is a long-form private sequence; do not cut away. It reserves the target’s Director slot, suppresses ordinary music, and includes timed client effects. `/alex moogcity stop [player]` ends it; `status` reports it. |
| `/alex director test alex_theme_rain [player]` | Tests the natural Alex-theme rain event. | Can reject when its audio gate or rain setup is unavailable. Leave the audio on. |
| `/alex director test alex_distant_glimpse [player]` | Tests the natural distant Alex glimpse. | Needs the event’s valid sighting/spawn setup. |
| `/alex director test tree_peek [player]` | Tests the Stalker tree-peek event. | A wooded outdoor area is the practical staging choice. |
| `/alex director test leafless_hard_cut [player]` | Tests the Leafless hard-cut event. | Requires its own natural setup; see integrations below if using Leafless Grove content. |
| `/alex director test moon_eyes_night [player]` | Triggers Moon Eyes at night. | Stage at night for the intended effect. While active, every loaded mob stops, clears its target, and stares along the moon's real celestial path until the night ends. |

### Director controls

`/alex director status` includes `showcaseSeen`, the number of scheduled EventTypes already recorded for that player.

- `/alex director status [player]` — prints pacing/status information for a player.
- `/alex director autonomous on|off|status` — toggles automatic controller triggers.
- `/alex director silent on|off` or `/alex director silent <seconds>` — suppresses Director events for controlled filming; 1–3600 seconds.
- `/alex director debug on|off` — turns Director diagnostics on or off.

## Entity and integration commands

| Command | What it does | Requirements and useful details |
| --- | --- | --- |
| `/spawnalex` | Publicly spawns a basic Alex at the command source. | `/spawnalex flint` gives her flint and steel; `/spawnalex egg` gives her a zombie spawn egg. This is a direct entity spawn, not a paced scare. |
| `/alexsummonhorror [player]` | Alex appears at a distance holding a spawn egg, then a random horror appears near the target. | This event uses monsters from the **Intense Horror** mod, so that mod must be installed. It works best above ground with open sky and a clear view. From console/no player target, it selects an online player. |
| `/alexpoppy [radius]` | Spawns Poppy Alex near a Herobrine. | Requires the Herobrine mod and a nearby recognized Herobrine entity; radius is 4–128, default 64. |
| `/alexstalker [radius]` | Spawns Stalker Alex near a Herobrine. | Same Herobrine integration requirements. |
| `/testdarkalex` | Spawns a static Dark Alex in front of the runner for texture checks. | Player-only visual test, not a scare. |
| `/testalexcompare` | Spawns normal and dark Alex side-by-side for texture comparison. | Player-only visual test. |
| `/testspirits [player]` | Triggers the Whispering Spirits circle. | **Whispering Spirits mod must be installed** and the target must be in a valid open area. |
| `/testleaflessgrovelightning [player]` | Strikes treetops in a Leafless Grove. | The target must be inside a Leafless Grove structure with found log-column treetops. |
| `/testanomalybridge [radius] [player]` | Attempts an Anomaly dark scene within radius 4–128 (default 56). | Uses natural checks. `/testanomalybridge force [radius] [player]` requests the forced variant, but the integration still needs usable world data. |

## Additional events

| Event | Command | What it does |
| --- | --- | --- |
| Mob Alert | `/testmobalert [player]` | Nearby hostile mobs turn on the player. |
| Log Player Sighting | `/testlogplayer [player]` | A player-shaped log appears beside a suitable log block. |
| Crawling Tunnel | `/testcrawlingtunnel [player]` | Alex crawls down a one-block-high mining tunnel toward the player. |
| Tunnel Pass-By | `/testtunnelpassby [player]` | Alex runs across the obvious opening or exit in a cramped tunnel. |
| Cave Silhouette | `/testcavesilhouette [player]` | Alex appears as a distant silhouette in a cave opening. |
| Window Peek | `/testwindowpeek [player]` | Alex slides past a suitable window. |
| Strip-Mining Trap | `/teststripminingtrap [player]` | Stages the fake miner and roadblock trap. Use `solo` for the debug-only companion bypass and `status` to inspect the scene. |
| Missing Favorite Item | `/missingitem trigger [player] [delay_seconds]` | Removes an inventory item, then returns it later. `triggerheld`, `status`, `return`, and `cancel` are also available. |
| Photo Memory | `/alexphoto capture` | Captures a hidden-perspective photo. Use `/alexphoto give` and `/alexphoto place` to stage a frame. Natural events can leave frames at a player's home. |
| Invitation Trail | `/alexinvitationtrail start [player]` | Starts the book-and-coordinate trail toward its void-descent payoff. `status`, `reveal`, `expire`, and `payoff` are available for filming. |
| Home Replica | `/alexhomereplica start [player]` | Creates a corrupted sky copy of the player's recognized home. `claimhere` marks a test home site; `status` and `cleanup` manage it. |
| The One Who Stayed | `/theonewhostayed start [player]` | A rare multiplayer Mimic copies a recently absent nearby player using saved identity, chat, and approved voice data. `status`, `candidates`, `selftest`, and `stop` help test it. |
| Anomaly Run Warning | `/testanomalyrunwarning [player]` | With **Anomaly Rephased** installed, Alex warns the player beside `a_happy`, then the Anomaly resumes its own chase. |
| Anomaly Shadow Tree Peek | `/testanomalytreepeek [player]` | Requires **Anomaly Rephased**. Alex appears in an Anomaly-linked tree-peek scene. |
| Anomaly Void Stairway | `/testanomalyvoidstairway [player]` | With **Anomaly Rephased** installed, creates the void-stairway scene. |
| From the Caves Billy Sleep | `/testfromthecavesbillysleep [player]` | With **From the Caves** installed, Alex approaches a sleeping player and hands the wake-up payoff to that mod's bed-drag scare. |
| From the Caves crossovers | `/testfromthecavesintegrations pet\|purified\|tunnel fixture\|natural` | Tests Pet Omen, Purified, But Not Saved, and Unfinished Tunnel. Use `fixture` for setup testing or `natural` to retain the normal gates. |
| Bed Occupied | `/bedoccupied trigger [player]` | Starts the bed-pressure event. `status`, `clear`, and `pressure set` manage it. |

### Natural-only and scripted events

- **Horse Freeze** stops a nearby horse.
- **Cave Ambiance**, **Sudden Breath**, and **Alex Breathing** are short sound events.
- **Fake Discord Notification** has five world milestones: Minecraft days 3, 15, 35, 70, and 120. Each milestone can play a notification for one player, then place one authored sign behind them. Each one happens once per world.

## Voice and memory features

### Voice echo

`/testvoiceecho [player]` replays a stored voice clip as an echo. It requires **Simple Voice Chat**, a ready voice-chat bridge, and at least one accepted captured clip. The debug command may use the target’s own clip in single-player/testing; ordinary gameplay tries to avoid immediately repeating the same speaker.

- `/testvoiceecho status` — capture, clip, rejection, loop-guard, and transcription diagnostics.
- `/testvoiceecho logs on|off|status` — voice debug logging.
- `/testvoiceecho analysis on|off|status` — optional analysis exports.
- `/alex voice trigger [player]` — same event under the `/alex` branch.
- `/alex voice transcription on|off|status|runonce` — controls transcription processing.
- `/alex voice transcription strict on|off|status` — when strict is on, playback requires an approved transcript.
- `/alex voice transcription key set <key>` / `clear` — runtime-only AssemblyAI key control. Treat keys as secrets; do not type or show them on stream.

### Chat, sign memory, and LLM controls

The sign system uses in-game chat and approved voice transcripts. It only uses Minecraft gameplay, chat, voice chat, configuration, and mod state.

- `/alexllm status` — reports whether the sign LLM is ready and prints diagnostics.
- `/alexllm setkey <key>` / `clear` — sets/clears the temporary runtime LLM key. Keep the key out of recordings and server logs.
- `/alexllm test` — previews a sign response for a sample message.
- `/alexllm memorypeek [player]` — shows a saved disk-memory snippet. Do not show this on public recordings without checking it first.

## Cleanup and troubleshooting

| Situation | Command/action |
| --- | --- |
| Stop Moog City | `/alex moogcity stop [player]` |
| Stop Massive Null | `/testmassivenull stop [player]` |
| Stop Cave Crying | `/testcavecry stop [player]` |
| Cancel climb scene | `/testclimbbolt cancel [player]` |
| Cancel sky fall safely | `/skyteleport cancel [player]` |
| Stop automatic Director events | `/alex director silent on` or `/alex director autonomous off` |
| Restore automatic Director events | `/alex director silent off` and `/alex director autonomous on` |
| Diagnose a scene | Use that event’s `status` command, then `/alex director status [player]` |

### Practical failure fixes

| Message/behavior | Usually means | Fix |
| --- | --- | --- |
| `NO_VALID_SPAWN`, `INVALID_SPAWN`, or `NO_VISIBLE_SPAWN` | The event cannot place its entity safely or secretly. | Clear floor/headroom, load the area, and give the player room behind or beside them. |
| `not_in_cave` / `no_valid_anchor` | Cave Crying needs a real cave and concealed anchor. | Move underground into a natural-feeling cave/tunnel. |
| `NOT_SLEEPING` / `NO_BED_SPAWN` | The sleep event has no sleeping target or viable reveal position. | Sleep in a proper bed with free space around it. |
| `NO_VALID_DOOR` | Door Knocking cannot select a suitable door. | Use a closed, accessible door at a small base. |
| `NO_CLIP` / `VOICECHAT_NOT_READY` | Voice echo has no accepted capture or its integration is not ready. | Install/configure Simple Voice Chat, speak long enough to capture a clip, then retry. |
| “mod is not loaded” | An optional integration is absent. | Install the matching mod or use a core event instead. |

## Command ownership and scope

The command system is intentionally split by feature: `EventDirector` owns pacing; individual Controllers own their distinct cave, line-of-sight, spawn, and geometry checks; optional integrations remain optional. That is why similarly named commands can have different requirements.

Use commands to stage a moment. In normal survival play, leave room between major manifestations so players can notice the hint or pressure before the reveal.
