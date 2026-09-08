# CKBuilder — Final Project Report

## 🎮 FiberSurvivors

**[▶ Play it here](https://zesty-youtiao-8586ae.netlify.app/)** — runs in the browser, no install, no wallet extension.

A top-down survivors-like where the coins you pick up are backed by **CKB moving over Fiber Network**. Clear a level, the hub pays you. Buy an upgrade card, you pay the hub. Cash out, the payment channel closes and everything settles on-chain.

Every reward and every purchase is an actual Fiber payment, in-run, in about a second.

> ⚠️ **Testnet.** Uses CKB testnet (Pudge) and test CKB from a [faucet](https://faucet.nervos.org/) here.

### The loop

```
fund a payment channel  ──►  fight through 10 levels  ──►  hub pays each level cleared
                                      ▲                            │
                                      │                            ▼
                              stronger build  ◄──  spend earnings on upgrade cards
                                      │
                                      ▼
                            cash out ──► channel closes, CKB settles on-chain
```

The first upgrade pick is free: you start with nothing to spend. After that, cards cost real CKB, and later levels pay 2–3× what early ones do. Spending to get stronger is how you reach the levels that pay.

### Playing

- **WASD** to move. Attacks fire automatically at the nearest enemy.
- Reach the goal at the end of the lane to clear the level. Ten levels, boss on the last one.
- Coins drop from kills. Every few coins, pick 1 of 3 upgrade cards — weapons or passive stats, slot-limited so you commit to a build.
- **Cash Out** any time from the results screen. It closes your channel and settles your balance to your wallet.

### First run

1. Press **Enter** on the boot screen — the game starts a Fiber node in your browser and dials the hub.
2. Copy your address from the funding screen and get test CKB from the [CKB faucet](https://faucet.nervos.org/).
3. Press **Play**. Opening the channel confirms on-chain and takes about a minute.
4. Play. Cash out when you're done.

Stuck? See **[Troubleshooting](docs/TROUBLESHOOTING.md)**.

### How it fits together

```
Browser (Netlify)                    VM (Google Cloud)
┌──────────────────────┐             ┌────────────────────────────┐
│  Unity WebGL build   │  https ───► │  Express reward backend    │
│  ┌────────────────┐  │             │   level claims, card       │
│  │ fiber-wasm node│  │             │   invoices, session seeds  │
│  └───────┬────────┘  │             ├────────────────────────────┤
└──────────┼───────────┘   wss  ───► │  fnn v0.8.0 (Fiber hub)    │
           │                          │   channels, payments      │
      localStorage                    └──────────┬─────────────────┘
      (node identity)                            │
                                            CKB testnet
```

Two things worth calling out:

**The node runs in the browser.** `fiber-wasm` compiled to WebAssembly, with its identity persisted in `localStorage`, so your node survives a page reload. This needs cross-origin isolation (COOP/COEP) for `SharedArrayBuffer` — which is why the Netlify `_headers` file matters.

**Rewards are server-authoritative.** Level payouts live only on the backend; the client never sees or sends an amount. Card prices come back as signed Fiber invoices, so a modified client can't name its own price. What the client *can* do is replay level 1 — that hole is known and bounded by a per-pubkey lifetime payout cap.

### Stack

Unity 6 (URP, WebGL) · Nervos CKB + Fiber Network · Node.js / Express · fnn v0.8.0 · Caddy · Netlify · Google Cloud

### Side deliverable

**[Fiber WebGL SDK](https://github.com/TranNhi27/FiberWebGLSDK)** — the Unity package that came out of making this work: an `IPaymentGateway` interface, the JS bridge to `fiber-wasm`, and a sample payment-flow scene.

---

## Docs

- **[Troubleshooting](docs/TROUBLESHOOTING.md)** — every failure mode hit during development, what causes it, and how to fix it
