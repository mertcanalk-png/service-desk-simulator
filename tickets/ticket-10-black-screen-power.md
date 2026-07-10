# Ticket 10 — Laptop Won't Power Up (Black Screen, Blinking Light)

> Self-directed simulator practice. Fictional data. Not paid work.

| Field | Detail |
|---|---|
| Priority | High (user fully unable to work, deadline pending) |
| Category | Hardware / Power |
| Reported symptom | Laptop won't come up. Screen black, power light slowly blinking continuously, power button unresponsive. Device is plugged in. |

---

## 1. Diagnosis

The reported signature — a slowly blinking power light with a black screen and an
unresponsive power button on a machine that is plugged in — indicates the device is
stuck in an unresponsive power state (a failed wake / hung power state) rather than
being genuinely without power. The light activity confirms power is present, so the
issue is the machine failing to resume, not a dead unit.

User steps already tried (repeated power-button presses) had not cleared it.

## 2. Root cause

The device was in a hung power state and would not resume.

Note: the exact origin of the hang (for example a failed sleep-to-wake transition
versus another firmware hang) was not separately confirmed. The resolving action
was a forced power cycle.

## 3. Action taken

- Assisted the user via chat.
- Removed all peripherals to rule out an external device holding the power state;
  this did not resolve it.
- Directed the user to press and hold the power button for ~30 seconds, forcing the
  machine to drain residual power and perform a hard restart.

## 4. Verification

- The machine restarted and booted normally.
- User confirmed the laptop was working.

## 5. Status

**Resolved** — forced power cycle restored normal boot.

---

## Lessons learned

1. **A blinking power light with a black, unresponsive screen is a power-state
   problem, not necessarily a dead machine.** The light confirms power is present,
   which points at a failed resume rather than a hardware-dead unit.

2. **Isolate external causes before the forced fix.** Removing peripherals first
   rules out an external device holding the state, so the forced power cycle is a
   considered next step rather than a first reflex.

3. **A 30-second power-button hold forces a hard power drain and restart.** It is the
   standard recovery for a hung power state, and it worked here — but it clears the
   state without confirming the underlying origin, so the specific cause remains
   unconfirmed.
