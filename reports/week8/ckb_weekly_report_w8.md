# **Builder Track Weekly Report — Week 8**

**Name:** Hayden

**Week Ending:** 07-12-2026

**Overall:** This week I fixed the VM networking issue from last week and finished testing the full payment flow inside the actual Unity WebGL build. I tested the complete
`ConnectPeer -> OpenChannel -> PayPeer -> CloseChannel` flow between the WebGL Node with the native Node. 

**Practical Progress**
- Confirmed browsers need /ws/ peer addresses, not /tcp/, because browsers can't open raw TCP sockets at all.
- Read Fiber's RPC docs.
- Learned that a resolved `sendPayment()`/`openChannel()` promise only means the *request* was accepted, not that the underlying operation finished, this is a repeating pattern across Fiber's async RPCs, not a one-off quirk.
- Found two early-success bugs: OpenChannel and PayPeer were both reporting done as soon as the request was accepted, not when the channel/payment actually finished. Fixed PayPeer by polling until a real terminal state, but 
OpenChannel needed several attempts to get a clean ChannelReady, so I'm not fully confident that one's solid yet. I will retest when integrating to the Game next week.
- Fixed the VM networking blocker: set the VirtualBox adapter to Bridged so the hub gets a real LAN IP the Windows build can reach.
- Got the full flow working inside the Unity WebGL build.

**Blockers / Deferred**
- Got one WASM panic after leaving a tab idle for a while, possibly from Chrome throttling background tabs, but didn't catch the actual panic log before reloading, so not confirmed. I will have an eye on this.
- Haven't started connecting any of this to actual gameplay yet, this week was just testing and fixing the integration.

**For My Final Game Project**
- The main open question from last week is answered: the full payment flow does work from inside a real Unity build.
- Next step is coding the Game Prototype and start wiring this into actual game events instead of a manual test UI. 

**Environment**
- `@nervosnetwork/fiber-js` v0.8.0, `@noble/curves` v2.x, `@ckb-ccc/core`
- `fnn` (Fiber Node) v0.8.0
- Unity 6000.0.32f1, WebGL build target, custom WebGL Template
- esbuild (bundling the JS Fiber bridge)
