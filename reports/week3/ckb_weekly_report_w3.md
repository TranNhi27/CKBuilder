# **Builder Track Weekly Report — Week 3**

**Name:** Hayden

**Week Ending:** 06-07-2026
- Overall: This week I gathered some concepts preparing for my onchain game project. I get to know xUDT where my game Extension script will attach to it, and Spore Protocol obviously to store game assets. The cool part 
about gaming on CKB is Fiber, I save some time this week to dig in Fiber and it turns out great with Fiber possibility of acting as a gasless bridge for provable onchain logic and reward.

**Courses Completed**
- Completed Phase 2: Lessons 10–12 of [Learning CKB Fundamentals](https://website-sooty-chi-72.vercel.app/)
- Started Phase 3: Lessons 13, 14, 15 of [Learning CKB Fundamentals](https://website-sooty-chi-72.vercel.app/)
- Ran [Create a Fungible Token](https://docs.nervos.org/docs/dapp/create-token) and [Create a DOB using Spore Protocol](https://docs.nervos.org/docs/dapp/create-dob) dApp
- Started Fiber Network Quick Start series

**Key Learnings**
- I gain much onchain contract knowledge this week:
  + **Counter Type Script**: the most impressive concept is 3-scenario state machine: Create, Update, Destroy. Also I can see Type script runs on both inputs and outputs practically
  + **Molecule Serialization**: understood the high-level concept of fixed-size vs dynamic layout and how CKB encodes on-chain data. The byte-level details need more hands-on work to fully internalize.
  + **CKB-VM Deep Dive**: RISC-V instruction set, Syscalls as the bridge between scripts and chain state, Cycle metering, Script execution isolation and security model
  + **xUDT Fungible Token Standard**: understand the difference between xUDT vs ERC-20, Owner mode vs normal mode. The most important thing to remember is Extension scripts which adding ruling layer to xUDT comparing to sUDT
  + **Spore Protocol (NFTs on CKB)**: Content stored directly on-chain in cell data (not IPFS), TypeID for globally unique Spore IDs, SporeData Molecule structure including content_type, content, cluster_id and 
CKB locked inside as guaranteed floor value
  + **Omnilock (Universal Lock Script)**: an interesting concept to learn about with single script handling 9+ auth modes via 1-byte flag, some Mode like 0x01 for Ethereum/MetaMask or 0x06 for M-of-N multisig for treasury/DAO governance.
  This is a completely fundamentally different approach compared to EVM Multisig, Vesting, or Crowdfund contract
  + **Fiber Network (Quick Dive)**: 
    - Payment channel lifecycle: Open (1 L1 tx) → unlimited off-chain payments → Close (1 L1 tx)
    - FundingLock + CommitmentLock scripts:  how channel funds are secured
    - Multi-hop routing via HTLC/TLLC (brief reading)
    - Fiber vs Lightning: multi-asset support, O(1) watchtower, cross-chain atomic swaps (brief reading)

**Practical Progress**
- Ran Lesson demos against CKB testnet
- Set up and ran 2 Fiber nodes locally on testnet
- Opened a payment channel between Node 1 and Node 2 then Transfer from Node 1 to Node 2: Open -> Transfer 100 CKB gasless -> Close Channel

**Environment**
- Fiber Node v0.8.0 installed and running on testnet
- ckb-cli v1.7.0 installed for key management
- fnn-cli for node interaction without raw JSON-RPC
