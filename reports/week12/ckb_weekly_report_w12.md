# **Builder Track Weekly Report — Week 12**

**Name:** Hayden

**Week Ending:** 08-09-2026

**Overall:** This week I tested payments properly and found the loop broke in several places in Game. 
I fixed those, settled the channel funding direction, and rebuilt the backend around it.
Some personal stuff came up this week as well, so I'm using the extension I'd asked for and aiming to land the final build as soon as it's solid.

**Practical Progress:**
- Game side:
  + Refactor Level asset: changed Ground asset and changed Camera angle setting.
  + Fiber Node Boot HUD: node boots, connects, shows pubkey and CKB address, then enables Play.
  + More Skills Asset: added more AoE type skills.
  + Skills HUD: 4 slots with cooldown sweep.
  + Fixed movement and auto-attack staying disabled after death, so run 2 was unplayable.
  + Pooling cleanup on level transition, one central release scheduler instead of per-object Update

- Fiber and Server side:
  + Added a dry run mode so the whole client-to-server flow is testable without a Fiber node running. Only the two calls that touch the node are stubbed.
  + Security pass on the backend: opening a channel now requires the player to
  already be connected to the hub, plus a cap on concurrent channels, rate
  limiting, and the RPC kept off the public interface.
  + Fix Server's bug: payments dying after the first death, the paid-levels
  record was tied to the wrong lifetime so restarting a run looked like a replay

**Objectives next week:**

- Deploy backend next to fnn, expose hub over wss, land payout flow in WebGL build. This is the first Todo next week.
- Fork SDK for xUDT, mint test tokens for hub liquidity
- Death / results screen, currently a loss restarts silently with no screen
- Upgrade cards priced in tokens, purchase path made async
- More levels, enemies and skills, final round as a boss

**Environment**:
- @nervosnetwork/fiber-js v0.8.0, @noble/curves v2.x, @ckb-ccc/core
- fnn (Fiber Node) v0.8.0
- Unity 6000.0.32f1, WebGL build target
- esbuild (bundling the JS Fiber bridge)
- Node.js 20 / Express (reward backend)
- Cloudflare Tunnel (exposing the hub over wss)
  
