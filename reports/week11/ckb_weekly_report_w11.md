# **Builder Track Weekly Report — Week 11**

**Name:** Hayden

**Week Ending:** 08-02-2026

**Overall:** This week was about closing the gap between "the SDK works" and "the game actually uses it." 
Payments are wired to game events, and the reward direction is designed and built, though not deployed yet. 

**Practical Progress:**

- Installed my own Fiber WebGL SDK into the game repo 
- Wired payments to game events using MockRunPaymentService.
- Wrote the backend server-authoritative reward design: a small Node service in
  front of the hub's RPC. The client reports which
  level it finished, not including any amount. The server owns the reward table, enforces claim ordering,
  rejects replays, checks elapsed time against wave timings, and issues per-level seeds at session
  start so a run can't be precomputed.
- Isolated that trust boundary behind one interface so a hold-invoice implementation can drop in
  later without touching game code.
- Game side: HUD (health, coins, skill bar, win/lose banner) and a Fiber diagnostics panel showing
  node pubkey, CKB address and session state. The banner shows the reward settling and then the
  payment hash, which is the clearest single-screen proof value moved.

**Blockers / Deferred:**
- Backend is written but not deployed to the VM yet, so the reward direction has only run against a
  local mock. First thing next week.
- No real WebGL build test this week: everything so far is Editor + mock.
- xUDT deferred till next week I will work on a fork of my SDK: 
  `funding_udt_type_script` on `open_channel`, `udt_type_script` on `send_payment`

**Objectives next week:**
Next week is going to be big and tough since it's the final week, but I'm aiming to deliver my best for it:

- Fork the SDK, add xUDT, mint test xUDT for the hub to hold as liquidity.
- Surface `local_balance` / `remote_balance` from `list_channels` for the token balance display.
- Deploy the reward backend alongside `fnn` and test a real payout to a WebGL build.
- Configure hub auto-accept co-funding so the server has outbound liquidity at run start.
- Split the upgrade shop into two currencies: coins in-run, tokens between levels.
- Add more levels, enemies and skills: I'm having 5-10 Levels in mind with the Final round having the Big Boss.
- Polish game with Feel Package.

**Environment:**

- @nervosnetwork/fiber-js v0.8.0, @noble/curves v2.x, @ckb-ccc/core
- fnn (Fiber Node) v0.8.0
- Unity 6000.0.32f1, WebGL build target, NavMesh
- esbuild (bundling the JS Fiber bridge)
- Node.js 18+ / Express (reward backend)
