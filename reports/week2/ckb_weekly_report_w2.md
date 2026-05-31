# **Builder Track Weekly Report — Week 2**

**Name:** Hayden

**Week Ending:** 05-31-2026
- Overall: This week I was aiming to finish till Chapter 10 but I ran into toolchain issues with ckb-std 0.16 about atomic instructions and C header dependencies so it took longer than I expected.

**Courses Completed**
- **Finished Lesson 6 in Phase 1 + Lessons 7-9 in Phase 2** of [Learning CKB Fundamentals](https://website-sooty-chi-72.vercel.app/)
- Completed chapters 4–9 of [Rust book](https://doc.rust-lang.org/stable/book/title-page.html)

**Key Learnings**
- This week, there are more hands-on experience with Cell, CCC and CKB Script:
  + **Cell Explorer and Indexer**: owner queries with findCellsByLock, contract queries with findCellsByType, only live cells are queryable, 4 indexer filter types including capacity range, data pattern, script, data length
  + **Hash Lock Script**: get to know no_std / no_main environment, CKB syscalls like load_script, load_witness, Source::GroupInput, Molecule serialization, Blake2b-256, Error codes as the only debugging channel from CKB-VM
  + **Cycle counting**: every instruction costs cycles, block limit is 3,500,000,000. Exceeding block limit will cause the txs to fail immediately althought the Contract logic is correct
  + **Script groups**: how CKB batches cells with identical scripts, 1 signature covers multiple cells
  + **Script Debugging**: VM error codes (negative) vs script error codes (positive), 5-step debugging methodology, ckb_debug! macro, ckb-debugger usage, 4 common bug patterns and importance of negative testing as of the case
 with happy path test
- **Rust**:
  + Ownership, borrowing, slices
  + Structs, enums, pattern matching
  + Error handling with Result and match
  + Traits, generics, iterators
  + Applied directly in no_std contract development
 
**Practical Progress**
- Wrote a Hash Lock Script in Rust from scratch following [Lesson 8](https://website-sooty-chi-72.vercel.app/lessons/08-hash-lock-script) which is compiled to RISC-V ELF binary.
- Resolved ckb-std 0.16 toolchain issues independently (atomic instructions, C header dependencies)
- Deployed, locked, and unlocked a hash-locked cell on CKB testnet:
  + Deploy tx: https://testnet.explorer.nervos.org/transaction/0x77e32acdd548ced876664f251f972062eff60575f4c8b3b5b1ecdc3c8bc1b969
  + Lock tx: https://testnet.explorer.nervos.org/transaction/0xa7e9c2babc39e915948503e7d53c9199d838308b93897ed0ba6971254d7f9997
  + Unlock tx: https://testnet.explorer.nervos.org/transaction/0xe247d89b87abbdecebaed5570f55fbf1dcfee1d7c6373ecac7bfd698f016d3ba
- Installed and verified ckb-debugger

**Environment**
- RISC-V toolchain (riscv64imac-unknown-none-elf) configured
- ckb-debugger installed
