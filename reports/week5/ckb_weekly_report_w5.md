# **Builder Track Weekly Report — Week 4**

**Name:** Hayden

**Week Ending:** 06-21-2026
- Overall: This week I interacted with famous protocols on CKB Testnet. Although I intended to warm up the Final Game Project this week but some interaction scripts took longer time than expected because of
errors and deprecated dependencies so I wrapped this week here. Next week I'll dig in some Fiber Game Project and start my own too.
- I also skipped Phase 4 of the Course which is related to Node Infrastructure for the time being, I might get back at it later.

**Courses Completed**
- Completed Phase 5: Lessons 21, 22, 23 of [Learning CKB Fundamentals](https://website-sooty-chi-72.vercel.app/)
- Made interaction scripts with RGB++, DEX, Spore Protocols on Testnet 

**Key Learnings**
- **RGB++ Crosschain Ownership**: it's really cool to see how real crosschain ownership can happen without Bridges,
RGB++ binds a CKB cell to a Bitcoin UTXO so the Bitcoin tx's confirmation finality effectively secures the CKB-side state. This enables the possibity of operating bussiness
and Protocol utilizing Bitcoin Liquidity
- **Order Cell Pattern**: An open order is its own cell on-chain, no central escrow. This Order Cell is effective for both xUDT and Spore which is mind-blowing, I really can feel the powel of 
reusable Scripts on CKB
- **SAY NO to MEV Bots**: "jumping the queue" just makes the late person's transaction fail and they don't lose money like on EVM
- **TYPE_ID-deployed contracts got updated bug**: @nervina-labs/ckb-dex hardcodes the DEX lock's deployment outpoint, but that contract got redeployed via TYPE_ID and the SDK's reference was never updated.
This one got me going around for quite a time

**Practical Progress**
- Ran Lesson 21 RGB++ explorer script against CKB testnet: after fixing a typo'd lock code_hash hardcoded in the lesson, the query went from returning mock data to finding real RGB++-locked cells
- For DEX:
  + scan-orders.ts: queries the indexer for live order cells using the DEX code_hash and decodes each via OrderArgs.fromHex()
  + make-orders.ts: listed 100 of my xUDT tokens for 50 CKB via a DEX order cell. Maker [txs](https://testnet.explorer.nervos.org/transaction/0x62462af4fa4f60d3fb245cd3d59dd3550c41c6f1713509d6635a7d3b42b138e7)
  + taker-order.ts: filled it from my second test wallet, completing the atomic swap. Taker [txs](https://testnet.explorer.nervos.org/transaction/0xe13d75404cd2460e0da9eea15b280f715a9f96bad4ada850ff69790546eb3262)
- For Spore:
  + scan-my-spores.ts: finds my own Spore cells by querying the indexer directly with the real codeHash (Collector's default getCells silently filters out anything with real data in it, so had to bypass that)
  + make-spore-order.ts: listed my Spore for 500 CKB via the same DEX order cell pattern. Maker [txs](https://testnet.explorer.nervos.org/transaction/0x5e241a84e2bf744d0bc6f565599e552441f2a995b09477af80050e21676ca1d7)
  + take-spore-order.ts: filled it from my second wallet, completing the swap (500 CKB to seller, Spore to buyer). Taker [txs](https://testnet.explorer.nervos.org/transaction/0x8633183a45ec61ab364a589569801d02f6aa01845110fef00c82d3182aad86ed)
  + Finally I verified the swap by re-scanning both wallets after so Spore confirmed gone from seller, confirmed in buyer's wallet with the same spore_id and capacity, content untouched

**Environment**
- Same Rust + RISC-V toolchain, ckb-cli, offckb CLI from prior weeks
- @nervina-labs/ckb-dex for DEX tx building + OrderArgs decoding
- @nervosnetwork/ckb-sdk-utils + ckb-sdk-core for manual cellDep/witness/signing fixes
- ckb-cli v1.7.0
- @ckb-ccc/core for indexer cell queries
