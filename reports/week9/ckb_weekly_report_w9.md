# **Builder Track Weekly Report — Week 9**

**Name:** Hayden

**Week Ending:** 07-19-2026

**Overall:** This week split into two halves. The first was the [Fiber hackathon](https://ckboost.netlify.app/campaign/0x3ba194e011b30817dfaf38bab946f55357a8bb32ef7dd1bbcf0608a59a132e6d),
where I packaged the Fiber integration work from Weeks 7-8 into a distributable Unity package, [FiberWebGLSDK](https://github.com/TranNhi27/FiberWebGLSDK), and submitted it.
The second was starting the Final Game Project (currently named FiberSurvivors, a top-down survivors-style prototype). The game half has little to *show* visually yet, but the core architecture is in with
player, enemies, spawning, stats, weapons and upgrades all exist as working systems. Fiber stays behind the `IPaymentGateway` interface for now and gets wired to actual game events over the next few weeks using the SDK.

**Practical Progress**
- FiberWebGLSDK: Restructured the Week 8 integration from loose scripts inside my game project into a real installable Unity package
- Game Project:
  + Assets: Sourced free, license-clean 3D assets (KayKit Adventurers and Skeletons, plus a forest environment pack)
  + Built the game's core systems: interface layer (IMovable/IDamageable/IEnemyAI/INavMover),
  a State Pattern top-down player controller,
  NavMesh enemies with pooling and composed AI,
  data-driven wave spawning (LevelSpawnData assets + scene markers), 
  PlayerStats with the genre stat vocabulary (Might, Area, Amount, Duration, Cooldown Reduction), 
  a slot-limited weapon/ability system (WeaponDefinition + WeaponInventory, projectile and damage-zone archetypes), and an UpgradeService with cost scaling and stack limits.
  
  => With the setup, I intend to make the Game Economy wrapping around this: players earn coins (xUDT or CKB) from kills, paid over Fiber from the server node, and spend them on upgrades. 
  Dying ends the round and forfeits unspent coins, so the pressure is on spending versus banking.

**Blockers / Deferred**
- The game has no Fiber calls in it yet.

**Objectives**
- Next week: connect the built systems into a playable loop (spawn → fight → earn → upgrade → die).
- After that: wire Fiber payments to game events (kills/waves).

**Environment**
- `@nervosnetwork/fiber-js` v0.8.0, `@noble/curves` v2.x, `@ckb-ccc/core`
- `fnn` (Fiber Node) v0.8.0
- Unity 6000.0.32f1, WebGL build target, NavMesh
- esbuild (bundling the JS Fiber bridge)
