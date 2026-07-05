# **Builder Track Weekly Report — Week 7**

**Name:** Hayden

**Week Ending:** 07-05-2026

**Overall:** This week I researched several existing projects that implement Fiber to lock in the direction for my final project. I studied Fiber Link and the Fiber WASM node, and analysed FiberQuest in depth. 
This research changed my architecture: the original tournament-pool model doesn't hold up, so I validated a browser-embedded Fiber node as the foundation instead.

**Material Covered**
- Cloned and read the source of `officeyutong/fiber-wasm-demo`, a reference implementation using `@nervosnetwork/fiber-js` 
- Confirmed via source (`Fiber` class constructor) that the WASM node uses Web Workers + `SharedArrayBuffer` + IndexedDB: genuine browser-native architecture.
- Read the native-node and WASM quick-start pages, which flagged a breaking node_id -> pubkey rename and JSON format changes in v0.8.0: this caught me out when officeyutong/fiber-wasm-demo didn't match my native node's version.
- Fiber Link: a community tipping/micropayment layer. Its architecture is a custodial hub which is an one always-online hub node holds the real funds, and a ledger (database) tracks each user's balance.
It lets users transact without running a node, but the tradeoff is custody.

**Practical Progress**
- Connected native Node to browser-based WASM node: `connectPeer`, `openChannel`, reach `CHANNEL_READY`, and complete a `sendPayment` on testnet. Finish full round trip, confirmed via both the client result and the Node's own logs.
- Built the Unity integration:
  - `IPaymentGateway` interface: (`Initialize`, `PayServer`, `GetNodeInfo`)
  - `FiberBridge.jslib`: a thin shim translating Unity's `DllImport("__Internal")` calls into calls on a JS bridge object, and routing callbacks back via `SendMessage`
  - `bridge.js`: bundled with esbuild, wrapping `@nervosnetwork/fiber-js` calls (`fiber.start`, `openChannel`, `sendPayment`, `nodeInfo`) with CKB address derivation ported from the reference demo
  - `FiberPaymentGateway.cs`: the single concrete adapter implementing the interface
- Built a minimal in-game test UI (pubkey/address display, Ready status, Pay button) calling only through `IPaymentGateway`
- Got the Fiber WASM node booting successfully **inside the Unity WebGL build**, with node pubkey and CKB address correctly displayed in-game: confirmed the full chain (C# -> jslib -> JS bundle -> Fiber WASM, and the callback path back) works nicely.

**Blockers / Deferred**
- My `fnn` native Node runs in an Ubuntu VM (VirtualBox), while the Unity build runs on the Windows host: these can't currently reach each other. I diagnosed the fix but didn't apply it this week yet because ran out of time.
- Because of the above, the in-Unity node hasn't been funded or completed an actual payment yet. I'll work on this next week.
- Noted a real gap in the bridge for later: the WASM node currently generates a fresh random keypair every session. It will need `localStorage` style persistence, same as the reference demo.

**For My Final Game Project**
- This week validated the riskiest technical assumption in my plan: a browser-embedded Fiber node really can run inside a Unity WebGL build with no player download, and the C# - JS bridge pattern works cleanly in both directions.
- Next concrete step: fix the VM networking, fund the in-Unity node, and get a real `PayServer` call succeeding from inside the build. This is the last unverified link before wiring this into an actual gameplay event.
- Because of some constraint my current plan for the game concept will be Player Node vs Game Server Node first, it's "Play-to-earn mechanics with instant payments" style because I want to make a single-person game:
  + `Fiber Link`: the architecture is nice, it's just doesn't really fit with Gaming since its mission is an always-online hub node holds the real funds for People who's offline.
  + `FiberQuest`: solid tournament + on-chain escrow model, but it's a desktop Electron app that runs the node natively and leans on an AI agent for payouts. Overall, it's heavier than I need.
  
**Environment**
- `fiber-wasm-demo` (React/TS reference), `@nervosnetwork/fiber-js` v0.8.0
- `fnn` (Fiber Node) v0.8.0
- Unity 6000.0.32f1, WebGL build target, custom WebGL Template
- esbuild (bundling the JS Fiber bridge)
