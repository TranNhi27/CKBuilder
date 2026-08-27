# **Builder Track — Extension Update**

**Name:** Hayden
**Date:** 08-27-2026

**Overall:** Quick status on the Final Game Project since Week 12: the money loop is now closed at both
ends (pay for cards, cash out at the end), the campaign loop is settled with a Boss fight at the end, and fixed some bugs related to WebGL Build.
Aiming to submit by 08-31.

**Progress since Week 12:**

- Payments:
  + Card purchases now run on server-signed Fiber invoices instead of client-priced
  keysend. Prices exported
  from Unity as the single source of truth.
  + Cash-out flow: player closes the channel from the results screen and gets a link
  to the settlement on the explorer.
  + Funding gate before Play: node boots, shows its address, waits until it's funded.
- Game:
  + Death / results screen, the Week 12 gap. A loss no longer restarts silently.
  + Boss encounter for the final round. 
  + Feel pass on casts, hits and deaths; more enemy types across the levels.
  + Fixed some VFX rendering magenta in WebGL.
- Addition for [FiberWebGLSDK](https://github.com/TranNhi27/FiberWebGLSDK) (code will later be pushed to the repo): 
  + Invoice, xUDT payments added to the gateway.
  + Fix CloseChannel now reports the settlement transaction.
  
**Remaining before submit:**
- Add more Game Levels, Hero Selection HUD and some more Player's Skills
- Test play loop
- Setup and deploy Server

**Note:** 
- Everything above is built and testable. 
One change of direction: rewards now pay in CKB rather than xUDT, and the amounts are scaled down so the hub's liquidity holds for a demo. The xUDT path stays in the SDK, it just isn't what the game uses.

**Environment:**
- @nervosnetwork/fiber-js v0.8.0, @noble/curves v2.x, @ckb-ccc/core
- fnn (Fiber Node) v0.8.0
- Unity 6000.0.32f1, WebGL build target
- esbuild (bundling the JS Fiber bridge)
- Node.js 20 / Express (reward backend)
- Cloudflare Tunnel (exposing the hub over wss)
