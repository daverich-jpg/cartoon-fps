# Block Blast playtest kit

A small, honest usability study you can run this week with 5–6 friends. It produces before/after evidence for the portfolio case study.

| Version | Link | What it is |
|---|---|---|
| **Before** | https://daverich-jpg.github.io/cartoon-fps/before/ | The visual overhaul with sound, *before* the UX research (commit `abbf56c`) |
| **After** | https://daverich-jpg.github.io/cartoon-fps/ | Current: aim-while-firing + aim assist, threat indicators, onboarding, star feed, end screen, pause/settings |

## 1. What we want to learn (research questions)

Each question maps to a change from the gap analysis.

| # | Research question | Change it tests |
|---|---|---|
| RQ1 | Can first-time players aim and shoot comfortably on a phone? | Aim while firing + aim assist |
| RQ2 | When players get hurt, do they know where it came from? | Damage arcs + edge chevrons |
| RQ3 | Can a first-timer get their first KO without help? How long does it take? | Teach-by-doing onboarding |
| RQ4 | Do players discover head shots (double damage) on their own? | Onboarding step 4 + BONK! |
| RQ5 | What do players think the gold Wishing Star is for? | Star feed |
| RQ6 | At the end, do players want to go again or share? | End screen + Share |

## 2. Setup

- **People:** 6 if you can (5 minimum). Nobody who has played it before.
- **Split:** 3 play **Before**, 3 play **After**. Each person plays only one version first, so neither "learns" the game from the other version. At the very end, let them try the other version for 1 minute and ask which they prefer.
- **Device:** their own phone, held sideways, sound on. If you lend your phone, open the link in a **private/incognito tab** so the first-run tutorial shows. (Tutorial progress, best score and settings are saved per browser.)
- **Time:** about 15 minutes each, in person if possible. Sit beside them so you can see the screen.
- **Kit:** a stopwatch (your phone), this sheet, and optionally a screen recording. Ask first.

**Be honest about scale:** 6 people won't give you statistics. They give you *directional* evidence and real quotes, which is what a portfolio case study needs. Write it up that way.

## 3. Session script (read roughly as written)

> "Thanks for helping! I'm testing a little game I designed, not you. There are no wrong answers, and if something's confusing that's useful for me. Please think out loud as you play: say what you're looking at, what you're trying to do, and anything that surprises you. I won't help while you play, but I'll answer everything after. Is it OK if I take notes / record the screen?"

Then:
1. Hand over the phone with the link open on the start screen. Say only: **"Play it however you like until you lose or want to stop."**
2. **Start the stopwatch when they tap Play.** Note the time of their **first KO**.
3. Stay quiet. If they're stuck for more than 30 seconds, say only "What are you trying to do?", and note that you prompted them.
4. Let them play until game over (or 5 minutes). If they want to, let them play again; *that's a data point*.
5. Ask the questions in section 4.
6. Let them try the other version for about 1 minute, then ask the preference question.

**Don't:** explain controls, say "try the head", point at things, or react when they do well or badly. Watch what they do, and write down what they say word for word.

## 4. Post-play questions

1. "In one sentence, what is this game about?"
2. "How did aiming and shooting feel? Anything awkward?" (RQ1)
3. "When you got hurt, did you know where it came from?" (RQ2)
4. "Did anything do extra damage?" Don't mention heads. (RQ4)
5. "What do you think the big gold star is for?" (RQ5)
6. "What did you want to do when the game ended?" (RQ6)
7. *(After trying the other version)* "Which one would you rather keep playing, and why?"

## 5. Note sheet (copy one per person)

```
Participant: P__   Version first: Before / After   Phone: ________   Played before? N
Time to first KO: ____ s        Prompted by me? Y / N (when: ____)
Wave reached: ____   KOs: ____  Played again unprompted? Y / N   Tapped Share? Y / N (After only)

Watch for (tally):
  Tried to aim and shoot at the same time and struggled     | ____
  Got hit and looked around confused / said "where?!"      | ____
  Aimed at heads on purpose (before I asked)               | Y / N   (wave __)
  Hesitated or got confused about controls                 | ____ (what: ________)
  Commented on the look, sound, or characters              | quotes below

Answers:
  Q1 about: ______________________________________________
  Q2 aiming: _____________________________________________
  Q3 hurt direction: _____________________________________
  Q4 extra damage: _______________________________________
  Q5 gold star: __________________________________________
  Q6 at the end: _________________________________________
  Q7 preference + why: ___________________________________

Best quote (word for word): "_____________________________________"
Biggest problem I saw: _________________________________________
```

## 6. Making sense of it (after all sessions)

1. **Fill in the comparison table.**

   | Measure | Before (P1–P3) | After (P4–P6) |
   |---|---|---|
   | Median time to first KO | | |
   | # who got a KO without a prompt | /3 | /3 |
   | # who aimed at heads unprompted | /3 | /3 |
   | # who knew where damage came from | /3 | /3 |
   | # who could explain the star | /3 | /3 |
   | # who played again unprompted | /3 | /3 |
   | Preferred version (all 6) | | |

2. **List the problems you saw.** Rate each by severity:
   - **3** blocks the goal
   - **2** slows or frustrates
   - **1** cosmetic

   Count how many people hit it. Fix anything that is severity 3, or severity 2 and seen in 2+ people.
3. **Pull 3–4 quotes**, at least one that's critical. Case studies with only praise read as unreliable.
4. **Decide** what to change next, and what you'll *leave alone* because the evidence didn't support it. (For example, build "defend the Wishing Star" only if people said the game lacks a goal.)

## 7. Messages to send

**Remote, if you can't sit with them** (less rich, still useful):
> Hey! I designed a little cartoon game and I'd love 10 minutes of honest feedback. Open this on your phone, turn it sideways with sound on, and play until you lose: [LINK]. Then reply with: 1) what the game is about in one sentence, 2) anything confusing or annoying, 3) what you think the gold star does, 4) your wave + KOs from the end screen. Brutal honesty welcome 🙏

For remote testers you can't time first KO yourself, so ask them to screen-record if they're willing.

**Just sharing for fun** (after testing):
> Made a little cartoon shooter, play it here: https://daverich-jpg.github.io/cartoon-fps/ (best on your phone sideways, sound on 🔊)
