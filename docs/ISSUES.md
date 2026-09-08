# Known Issues & Common Problems

FiberSurvivors runs on real testnet payments in your browser, which means a few things can go sideways that have nothing to do with your build or your internet. This page covers what you might run into and what to do about it.

If something isn't listed here, [open an issue](../../issues) and include what you saw in the browser console (F12 → Console tab) if you can.

---

### The game gets stuck / stops responding, especially after cashing out

**What's happening:** After a cash-out, the payment node sometimes ends up in a bad state and can't open a new channel.

**Fix:** Reload the page (F5). This is expected right now, not a sign something's broken on your end — the game should reload for you automatically a few seconds after your cash-out settles, but if it doesn't, do it manually.

---

### "Insufficient balance" or a card won't buy even though I have CKB

**What's happening:** Your wallet balance and your in-channel balance are two different things. Only the CKB actually inside your payment channel can be spent on cards — your wallet can be full while your channel is empty.

**Fix:** Cash out (this returns everything to your wallet and closes the channel), then play again — a fresh channel will be funded properly. If you're on a brand-new browser profile or incognito mode, you'll also need to fund that profile from the faucet first.

---

### The game won't get past "Waiting for funds..."

**What's happening:** The game is watching your testnet CKB address and hasn't seen a deposit yet.

**Fix:**
1. Copy the address shown on screen.
2. Get free testnet CKB from the [Nervos faucet](https://faucet.nervos.org/).
3. Wait about 30–60 seconds — the game checks every 5 seconds.

---

### "Opening channel..." has been sitting there for a while

This step confirms on-chain and normally takes **up to about two minutes**. That's expected, not frozen. If it's been much longer than that, reload the page and try again.

---

### A red error mentioning "Init message" or "handshake"

**What's happening:** A connection hiccup between your browser and the game's server. The game retries automatically a few times.

**Fix:** If it still fails after retrying, reload the page. This usually clears it.

---

### "Fiber panicked, please refresh page"

Exactly what it says — the payment node crashed and needs a fresh start.

**Fix:** Reload the page. Your progress in the current run is lost, but your CKB is safe (it's either still in your wallet or still in your channel on-chain).

---

### Nothing happens when I press Play / the buttons don't respond

**Fix, roughly in order:**
1. Reload the page.
2. Try a different browser (Chrome or Edge work best — Safari and some mobile browsers don't fully support the tech this game uses).
3. Make sure you're not in a browser mode that blocks cross-origin isolation or WebAssembly (some privacy extensions do this).

---

### I see errors mentioning "binance" or "tonbridge" in the console

Not this game — that's a wallet browser extension (like a crypto wallet plugin) injecting itself into every page you visit. Safe to ignore, or test in a private/incognito window without extensions.

---

### Is my money safe if something goes wrong?

Yes. Your CKB either sits in your wallet or sits in your payment channel — both are on-chain and yours regardless of whether the game's UI is behaving. Cashing out is the only way to close a channel and move its balance back to your wallet, and it's always available from the results screen while a channel is open.

---

### This is testnet, right?

Yes — this uses Nervos **testnet** CKB (Pudge), obtained for free from a faucet. No real money is involved anywhere in this game.
