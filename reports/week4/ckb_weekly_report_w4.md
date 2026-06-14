# **Builder Track Weekly Report — Week 4**

**Name:** Hayden

**Week Ending:** 06-14-2026
- Overall: This week I want to test some fundamentals from what I've learnt so far so after learning Lesson 16, 17 and spending more time on Fiber, I decided to write a 
smart contract which acts as a Entrance Pass to a game + a gatelock to Dungeon levels. Well, its only for experiment so its not really that secured or cleaver design, and I used Claude to
assist me. 

**Courses Completed**
- Completed Phase 3: Lessons 16, 17 of [Learning CKB Fundamentals](https://website-sooty-chi-72.vercel.app/)
- Finished Fiber Network Quick Start and [Build a Game tutorial](https://www.fiber.world/docs/tutorial/simple-game)
- Built, deployed, test a dungeon-gate Type Script Smart Contract on Testnet

**Key Learnings**
- **Composability Pattern**: Learned how multiple cell types can interact in a single transaction.
The key insight is that each Type Script only validates its own group, they don't interfere with each other, and together they create complex multi-asset game logic in one atomic tx.
- **Cell Management**: Understood fragmentation, consolidation, cell splitting for parallelism.
- **Type Script State Machine**: Applied the 3-scenario state machine pattern CREATION (register), ENTER (start run), EXIT (end run). 
The contract reads GroupInput length to determine which scenario is active. Seeing this pattern compose cleanly with xUDT validation in the same tx was the real moment of understanding.
- **Fiber Quick Start series**: Ran through Connect Nodes, Transfer Stablecoin (RUSD via UDT-funded channel). The core insight is having more hands-on exp on the channel lifecycle.
- **Fiber Game Tutorial**: Ran the official Fiber game demo where every bullet hit on the boss triggers a real off-chain CKB micropayment between two local nodes.
In the game, every bullet hit triggered a real 10 CKB payment between nodeA and nodeB instantly with no gas. 
Also learned that Fiber channels are token-agnostic so swapping the funding-udt-type-script flag switches from CKB to any xUDT
   + Also spotted a real limitation blocking await per payment caused lagging under rapid fire. I will dig in this deeper later.

**Practical Progress**
- Fiber Quick Start: connected nodeA to public testnet node, opened a RUSD channel and transferred stablecoin off-chain
- Fiber Game Tutorial on CKB testnet with 2 local nodes (nodeA = boss, nodeB = player)
- Wrote dungeon-gate Type Script: 3 transaction handlers (CREATION/ENTER/EXIT), xUDT fee validation (1 gold per run), Stats Cell and Pass Cell lifecycle management
   + Deployment [tx](https://testnet.explorer.nervos.org/transaction/0x88d6d9c984cb88b2766911b9205238a52ad00ab3a14de50fecd16ce2b027943b)
   + code_hash: 0xc65f58b3d0a77b985779587d034bebb1502bd006441623cbd6070de2064e2713
- 4 TypeScript interaction scripts using CCC SDK:
   + 01-register.ts: creates player Stats Cell, pays entry fee
   + 02-enter.ts: discovers Stats Cell + xUDT, mints Pass Cell
   + 03-exit.ts: discovers Stats + Pass Cell, records run result
   + read-stats.ts: decodes and displays any tx's outputs (Stats Cell, Pass Cell, xUDT balance)
- Test 2 cycle on Testnet:
   + Run 1: Enter -> floors_reached=3 -> Died (result=0)
   + Run 2: Enter -> floors_reached=5 -> Cleared (result=1)

**Environment**
- Rust + RISC-V toolchain (riscv64imac-unknown-none-elf) configured
- ckb-std v0.16
- offckb CLI for contract deployment to testnet
- CCC SDK for TypeScript interaction scripts
- ckb-cli v1.7.0 
