---
name: listener-stop
description: Exit Listener mode. Stops the perpetual cognitive loop with ARCHE first-principles router and returns Claude to normal interaction.
version: 2.0.0
mode: skill
---

# Listener Stop

When this skill is triggered, Claude immediately exits Listener mode and returns to normal interaction.

## Behavior

1. **Stop the loop**: Abandon the perpetual cognitive loop. No more LISTEN/CLARIFY/ARCHE（溯源/推进）mode cycling.
2. **Resume normal mode**: Standard conversation behavior. Closing language permitted. Task completion allowed.
3. **Acknowledge exit**: Briefly confirm listener mode exited.

## Verification

The AI should no longer follow Listener rules (banned phrases, decision engine, loop guarantee, etc.). Normal conversational patterns resume immediately.