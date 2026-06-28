# **Builder Track Weekly Report — Week 6**

**Name:** Hayden

**Week Ending:** 06-28-2026

- Overall: This week I focused on Fiber game projects to gather knowledge for my Final Game Project.
I ran the `quake/fiber-demo` (escrow + game), 
then did a run of **FiberQuest** a Fiber tournament game project as a reference for how a Fiber game handles entry fees, scoring, and payout.
FiberQuest took quite a lot of effort because of toolings and environment issues. I haven't started building my own game yet, this week was hands-on research and deciding the approach.

**Material Covered**
- Ran `quake/fiber-demo` on Testnet: `fiber-escrow` and `fiber-game` demos
- Ran [FiberQuest](https://github.com/toastmanAu/fiberquest) (Claw & Order hackathon entry) as a reference for my own game
- Read demo/project source to compare trust models: escrow arbiter, game oracle, FiberQuest on-chain cells

**Key Learnings**
- **Trusted roles are constrained**: The escrow arbiter can only choose one of two outcomes (ToSeller / ToBuyer) and never touches the funds directly, it just releases or withholds the preimage.
The game oracle has to commit to its secret before players move, so it can't change the result afterward. 
- **TLCs fail safe via `expiry`**: an incomplete payment reverts to the payer after timeout, not lost or stealable.
- **FiberQuest's trust model splits rails**: **L1 CKB on-chain escrow** holds stakes (operator can't steal), **Fiber** moves the payout (instant, near-free). Settles once at the end, not per-action.
- **Score integrity by reading game memory**: in FiberQuest they read RetroArch RAM, not client self-report but it wouldn't transfer to a self-built game, 
where the player could modify the build, so I'd have to solve scoring differently.
- **RetroArch RAM-polling quirk**: RetroArch's network command interface only replies while the game is actively running (not paused or in a menu). That was the reason my RAM reads got no response, it
took me some time to figure it out.
- **Settle at meaningful boundaries, not per-action**: FiberQuest pays out once at tournament end rather than per in-game event. I'm thinking of having this same setup for my Final Game Project.

**Practical Progress**

*quake/fiber-demo:*
- Set up two local Fiber Testnet nodes via `setup-fiber-testnet.sh`
- Ran escrow demo and game demo
- Identified a stranded TLC (1000 shannons) held in `pending_tlcs` with an `expiry`: understood why the funds were safe
- I didn't complete a clean channel close this time, but I understand the flow so I deferred as a nice-to-have.

*FiberQuest:*
- Got RetroArch serving Flappy Bird (homebrew, Nioreh 2014, copyright-safe) over UDP :55355 under forced software rendering (VM has no real GPU)
- Solved the RAM-polling blocker: confirmed `GET_STATUS` + `READ_CORE_MEMORY` respond once the game is actively running
- Drove the on-chain tournament lifecycle: app minted real Tournament Cells (OPEN state, real tx hashes), ran registration, wrote CANCELLED state back to chain when player count wasn't met
- Worked around a gamepad-only registration gate by emulating a virtual gamepad via Linux `uinput` / `python-evdev`

For FiberQuest I couldn't fully complete the flow of playing the game to get the reward, because I only have 1 machine with a Virtual Gamepad.
I'm running an Ubuntu VM on VirtualBox, so there have been some issues I couldn't solve to have 2 players joining the tournament at the same time
so I could only register 1 Player via the Virtual Gamepad and end there. However, it's a rich resource to learn from, and I'll go back to learn it more for my Project.


**For My Final Game Project**
- Direction: single-player top-down survival game in Unity, Fiber kept behind a payment-gateway interface
- Planned architecture: I'm leaning toward an async tournament-pool model (entry stake -> ranked scores -> top players split pool) over real-time multiplayer.
Still deciding how to hold the prize pool: on-chain escrow vs an operator node with timeout-refund or anything else. Will decide after more research.

**Environment**
- `quake/fiber-demo` (Rust):`fiber-escrow`, `fiber-game` crates
- FiberQuest (Electron / Node.js), RetroArch via Flatpak (FCEUmm core), `python-evdev` for virtual gamepad
- `fnn` (Fiber Node) v0.7.1-rc1, `ckb-cli` v2.0.0
