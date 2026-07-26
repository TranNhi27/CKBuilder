# **Builder Track Weekly Report — Week 10**

**Name:** Hayden

**Week Ending:** 07-26-2026

**Overall:** This week was all about Game side in the Final Game Project (FiberSurvivors), mostly closing gaps that were left over from week 9's first architecture pass. 
Instead of building new stuff I spent most of the time making sure the systems that already existed actually worked together and held up when i actually tested them, 
stuff like the win/lose flow, the upgrade card popup, and a pooling pass that ended up surfacing a couple real bugs along the way.
Fiber is still haven't wired to the Project, deferred so the core loop is solid before I hook payments into it. 

**Practical Progress:**
- Got a playable loop set up for Level 1 (spawn → fight → earn → upgrade → die).
- Built the upgrade card popup: the 3 cards you pick from when you level up, spending in-game coins earned from kills. 
This is the piece that'll plug into xUDT/CKB once Fiber payments are wired in.
- Wrote up a first batch of real upgrades cards: health, damage, fire rate, movement speed, skill, etc
- Also cleaned up some visual/pooling bugs found during testin

 **Blockers / Deferred:**
- Due to time constraint, I can't wired Fiber in this week.

**Objectives next week:**
- Game side: HUD (health/coins), win/lose screens, Fiber's UI.
- Fiber: wiring Fiber payments to actual game events using the SDK.

**Disclaimer:** I'm using some paid assets to speed up development and make the game look nicer, currently Feel and the Vefects Effect Pack. 
This means the full game source likely can't be open sourced later, since those assets come with their own licensing restrictions.

**Environment:**
- @nervosnetwork/fiber-js v0.8.0, @noble/curves v2.x, @ckb-ccc/core
- fnn (Fiber Node) v0.8.0
- Unity 6000.0.32f1, WebGL build target, NavMesh
- esbuild (bundling the JS Fiber bridge)
