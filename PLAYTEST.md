# Block Blast playtest kit

A small usability study of the **current build**, run with friends on their own phones. It tells us what to fix next, and the findings feed the portfolio case study.

**Game link:** https://daverich-jpg.github.io/cartoon-fps/

**How it works:** test with 5 people → turn notes into findings → fix the top issues → test again with new people. Each pass is a *round*.

---

## 1. What we're testing

The current build includes these features. Each research question checks whether one of them works for real players.

| # | Research question | Feature it checks |
|---|---|---|
| RQ1 | Can first-time players get their first KO without any help? How long does it take? | First-run onboarding (look → walk → fire → heads) |
| RQ2 | Can players aim and shoot comfortably on a phone? | Hold FIRE and slide to aim; touch aim assist; on-target crosshair |
| RQ3 | When players get hurt, do they know where it came from? | Tangerine damage arcs; edge chevrons for nearby Grinnies |
| RQ4 | Do players use head shots on purpose? | Onboarding step 4; "BONK!" on head hits |
| RQ5 | What do players think the gold Wishing Star is for? | Sparkles fly from each KO into the star |
| RQ6 | At game over, do players want to go again or share? | End screen: stats, best score, Share button |
| RQ7 | Does anything feel broken, slow or uncomfortable on their phone? | Performance, layout, sound, pause/settings |

**Baseline:** my own notes from playing the earlier build (https://daverich-jpg.github.io/cartoon-fps/before/) go in the Baseline section of the log (section 7). They're useful context, but they're one person who already knew the game. Friends' sessions are the real data.

---

## 2. Setup

- **Who:** 5 people per round, people who haven't played before. A mix helps: some who game a lot, some who rarely do.
- **Device:** *their own* phone, held sideways, sound on.
  - If you lend your phone, open the link in a **private/incognito tab**. The tutorial only shows on a player's first visit, and best score and settings are saved in the browser.
  - iPhone: check the silent switch is off, or there'll be no sound.
- **Time:** about 15 minutes each, in person if possible. Sit beside them so you can see the screen.
- **You need:** a stopwatch (your phone), a copy of the note sheet (section 5), and optionally screen recording (ask first).

> Honest framing for the case study: 5 people won't give you statistics. They give you *directional* evidence, patterns that repeat, and real quotes. That's normal for usability testing. Say so in the write-up.

---

## 3. Session script

**Intro (read roughly as written):**
> "Thanks for helping! I'm testing a game I designed, not you. There are no wrong answers. If something's confusing, that's exactly what I need to know. Please think out loud while you play: what you're looking at, what you're trying to do, anything that surprises or annoys you. I won't help while you play, but I'll answer everything afterwards. Is it OK if I take notes or record the screen?"

**Play:**
1. Hand over the phone with the game open on the start screen. Say only: **"Play however you like until you lose or want to stop."**
2. **Start the stopwatch when they tap Play.** Write down the time of their **first KO**.
3. Stay quiet. If they're stuck for 30+ seconds, say only *"What are you trying to do?"* and mark that you prompted them.
4. Let them play to game over (or 5 minutes). Note what they do on the end screen *before* you say anything.
5. If they choose to play again, let them. That's a good sign; note it.

**Don't:**
- explain the controls
- hint ("try the head")
- point at the screen
- react when they do well or badly

Watch what they *do*, and write down what they *say* word for word.

---

## 4. Post-play questions

Ask in this order. Questions 4 and 5 don't name the answer, so you don't lead them.

1. "In one sentence, what is this game about?"
2. "How did aiming and shooting feel? Anything awkward?" *(RQ2)*
3. "When you got hurt, did you know where it came from?" *(RQ3)*
4. "Did anything do extra damage?" *(RQ4; don't mention heads)*
5. "What do you think the big gold star is for?" *(RQ5)*
6. "What did you want to do when the game ended?" *(RQ6)*
7. "Was anything slow, glitchy, hard to see, or uncomfortable on your phone?" *(RQ7)*
8. "If you could change one thing, what would it be?"

---

## 5. Note sheet (one per person)

```
Round: __   Participant: P__   Phone/browser: ______________   Plays games: often / sometimes / rarely

TIMING
  Time to first KO: ____ s            Prompted by me? Y / N  (when: ____)
  Finished onboarding? Y / N           Stuck on step: look / walk / fire / heads / none
  Wave reached: ____   KOs: ____   Hit %: ____   (from the end screen)

ON THE END SCREEN (before you speak)
  Played again unprompted? Y / N       Tapped Share? Y / N       Looked at stats? Y / N

TALLIES (mark each time you see it)
  Struggled to aim while shooting ............................. | ____
  Got hit and looked around confused / said "where?!" ......... | ____
  Aimed at heads on purpose before Q4 ......................... | Y / N  (wave __)
  Confused by a control or prompt ............................. | ____  (which: ________)
  Performance / layout / sound issue .......................... | ____  (what: ________)
  Opened pause or settings .................................... | Y / N  (changed: ________)

ANSWERS
  Q1 about: _____________________________________________________
  Q2 aiming: ____________________________________________________
  Q3 hurt direction: ____________________________________________
  Q4 extra damage: ______________________________________________
  Q5 gold star: _________________________________________________
  Q6 end of game: _______________________________________________
  Q7 phone issues: ______________________________________________
  Q8 change one thing: __________________________________________

Best quote (word for word): "______________________________________"
Biggest problem I saw: ___________________________________________
```

---

## 6. Turning notes into fixes

Do this after each round of 5.

**Step 1: Fill in the scorecard.**

| Measure | Target | Round 1 | Round 2 |
|---|---|---|---|
| Median time to first KO | under 45 s | | |
| Got first KO with no prompt | 5/5 | /5 | /5 |
| Finished the onboarding | 5/5 | /5 | /5 |
| Aimed at heads before Q4 | 3/5+ | /5 | /5 |
| Knew where damage came from (Q3) | 4/5+ | /5 | /5 |
| Could explain the gold star (Q5) | 3/5+ | /5 | /5 |
| Played again unprompted | 3/5+ | /5 | /5 |
| Reported a performance/layout issue | 0/5 | /5 | /5 |

The targets are a starting point. Adjust them if they turn out unrealistic, and say so in the case study.

**Step 2: List every problem** you saw or heard. Give each one a severity and count how many people hit it:
- **3, blocker:** stops them reaching their goal (e.g. can't figure out how to shoot)
- **2, major:** slows them down or frustrates them (e.g. keeps getting hit from behind)
- **1, minor:** cosmetic or a one-off

**Step 3: Decide.**
- **Fix now:** any severity 3, and any severity 2 seen in 2+ people.
- **Watch:** severity 2 seen once, or severity 1 seen in 3+ people.
- **Leave:** everything else. Write down *why* you're leaving it; a case study that shows restraint reads well.
- Only add big new features (e.g. a "defend the Wishing Star" mode) if the evidence asks for it. For example: people can't say what the game's goal is (Q1), or don't play again (RQ6).

**Step 4: Log it** in section 7, then fix, then run Round 2 with *new* people to check the fixes worked.

---

## 7. Findings log

### Baseline: my own notes on the earlier build (before/)

- 
- 

### Round 1 (date: 2 Oct 2026, build: `commit 13416c8`)

P1 and P2 played remotely and answered the questions; David added an expert review of the UI.

| # | Problem | Severity | Seen by | Evidence (quote / observation) | Decision | Fix (commit) |
|---|---|---|---|---|---|---|
| 1 | Gold star's purpose not understood; the intro text was doing the teaching | 2 | 2/2 | P2: "I have no idea". P1: "I would've been confused if I didn't read that" | **Fix:** the star becomes the reward. A HUD star meter fills with each KO; clearing a wave grants a wish | see below |
| 2 | No reward for clearing waves, no enemy variety; "just keeps getting harder" | 2 | 1/2 (+ research gap) | P1: "some reward for completing waves… no rewards or other types of enemies" | **Fix:** wish upgrades (pick 1 of 3); Zippy Grinnies from wave 3, Big Grinnies from wave 5 | see below |
| 3 | Character animation feels off | ? | 1/2 | P2: "the character animation?" Unclear what or why | **Watch:** ask P2 which character and what felt wrong before changing anything | n/a |
| 4 | Title stars render with several stacked shadows | 1 | expert | David: "one individual star has several shadows. It doesn't look natural" | **Fix:** single outline + one drop shadow | see below |
| 5 | Portrait HUD: pause/sound squashed into ovals; Wave/KO pill wraps and floats over the scene | 2 | expert | David's screenshot | **Fix:** stats moved under the health bar as plain outlined text; icon buttons can't shrink; wish meter centred | see below |

**Best quotes:**
- "It just keeps getting harder and harder with no rewards or other types of enemies" (P1)
- "Shooting blobs" (P2, describing the game; it doesn't yet read as a world with a goal)

**What worked (keep):**
- P2's reaction to the end screen and stats: "love"

**Open questions for Round 2:**
- Can new players say what the gold star does *without* reading the intro? (Target: 3/5)
- Do players feel rewarded after a wave? Ask "What happened when you cleared a wave?"
- Do players notice the new Grinnie types, and do they change how they play?

### Round 2 (date: ______, build: `commit ______`)

| # | Problem | Severity | Seen by | Evidence | Decision | Fix (commit) |
|---|---|---|---|---|---|---|
| 1 | | | /5 | | | |

---

## 8. Messages to send

**Asking someone to test in person:**
> Hey! I designed a little cartoon game and I'd love 15 minutes of you playing it while I watch. You'll be testing the game, not being tested 😄 Free sometime this week?

**Remote, if you can't sit with them** (less detail, still useful; ask for a screen recording if they're up for it):
> Hey! I designed a little cartoon game and I'd love honest feedback. Open this on your phone, turn it sideways with sound on, and play until you lose: https://daverich-jpg.github.io/cartoon-fps/
> Then reply with:
> 1) what the game is about, in one sentence
> 2) anything confusing, awkward or annoying
> 3) what you think the gold star does
> 4) your wave + KOs from the end screen
> 5) one thing you'd change
> Brutal honesty welcome 🙏

**Just sharing for fun** (after testing):
> Made a little cartoon shooter, play it here: https://daverich-jpg.github.io/cartoon-fps/ (best on your phone sideways, sound on 🔊)
