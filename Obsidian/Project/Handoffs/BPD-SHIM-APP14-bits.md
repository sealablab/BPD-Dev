

1) TOP level entity, has four Inputs/Outputs
2) SHIM level: has four Inputs/Outputs
3) APP LEVEL: has **three** (user modifiable Inputs) has **three** user modifiable outputs - but heres the pitch

4) by default, the SHIM will / should have special access to the APP levels __state__ register (this is different than
__status__ register)
- the __Status__ register is intentioally exposed / defined by APP (that is its goal)

- the __state__ register is the authoritatve six-bit state encoding that the FORGE application structure dictates.

### APP LEVEL
This gives us 14 bits that the **SHIM** layer can
- 8 bit __STATUS__ register (intentionally app specific
- 6 bit __STATE__ register (per FSM observer spec)

### SHIM LEVEL 
takes APP LEVEL 'STATE' and 'STATUS' bits and
- mechanically maps them to 'OuputD'

The real question, what is the most useful voltage mapping scheme that will 'render well' on an oscilloscope ? :) 


> ## Wait a second though, i think there is a potential combination that

1) Assumes that there is some linear ordering to the internal state machine representation - if not, we may consider now to be the time to enforce one 


2) assume that APP:STATUS[7] -is- a fault  (we can suggest and or enforce this)

3) use that knowledge to set the whole 'Scope goes negative on FAULT' property up intentionally 
4) Maybe can, with those assumptions or constraints: create a way to pack OutputD such that:
5) progressions through the state machine will convey linear increments of, say, 200mv 
6) APP:STATUS[7] forces oscilloscope reading negative
7) 8-bits of APP specific state look like 'noise' at the various levels of the main state transitions

