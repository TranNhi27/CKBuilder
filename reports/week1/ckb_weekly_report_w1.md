# **Builder Track Weekly Report — Week 1**

**Name:** Hayden

**Week Ending:** 05-24-2026

**Courses Completed**
- [Introduction to Nervos CKB](https://docs.nervos.org/docs/ckb-fundamentals/nervos-blockchain)
- **5/6 Lesson in Phase 1** of [Learning CKB Fundamentals](https://website-sooty-chi-72.vercel.app/)
- Skim section 1, 2, 3 of [Rust book](https://doc.rust-lang.org/stable/book/title-page.html)

**Key Learnings**
- Developed a deep understanding to CKB theory and fundamentals:
  + **Cell Model structure**: capacity, data, lock, type
  + **Transaction structure**: 6 arrays, how fees work, time locks, block reference, transaction lifecycle, signature in witnesses array
  + **CKByte economics**: dual-purpose token, minimum 61 CKB cell, capacity formula, primary vs secondary issuance, Nervos DAO as inflation shelter
  + **CCC SDK basic**: ClientPublicTestnet, SignerCkbPrivateKey, findCellsByLock, completeFeeBy, sendTransaction
  + **Learn the difference between CKB and Ethereum**: Account Model vs Cell Model, gas vs capacity, and storing on network requires locking and releasing CKB while on Ethereum data stays there forever
  + **NC-MAX consensus**: Eaglesong PoW, selfish mining resistance, orphan/uncle blocks, dynamic block intervals
- **Rust**: This week I only skimmed through 3 sections but thanks to Cairo knowledge the ownership concepts feel similar in a way that I think I could get it quickly in order to start some smart contract work next week:
   + Variables and mutability
   + Data types
   + Functions
 
**Practical Progress**
- Set up a **local CKB dev** node successfully
- **Deploy a test contract** to local dev node
- Queried **Live Cells** from CKB testnet
- Built and ran TypeScript scripts using **CCC SDK on testnet**


**Environment**
- **offckb** installed for local devnet
- **CCC SDK (@ckb-ccc/core)** installed and working
- **Rust and Cargo** installed

