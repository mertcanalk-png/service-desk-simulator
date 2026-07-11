# Ticket 13 — Floor 2 Network Dropping Intermittently

> Self-directed simulator practice. Fictional data. Not paid work.

| Field | Detail |
|---|---|
| Priority | High (multiple users affected, business-critical calls dropping) |
| Category | Network / Infrastructure |
| Reported symptom | Users on Floor 2 lose network for ~30 seconds every few minutes, then reconnect. Affects both wired and wireless. Other floors unaffected. Pattern started this morning. |

---

## 1. Diagnosis

Two details defined the scope:

- The problem is limited to **Floor 2**; other floors are unaffected.
- It affects **both wired and wireless** connections on that floor.

Wired and wireless failing together on a single floor points to a component upstream
of both, rather than to an access point (which would affect wireless only) or
individual devices. On one floor, that shared upstream component is the floor's
network switch. The fault was therefore isolated to the Floor 2 switch.

This was confirmed rather than assumed: the server room overview showed 7 of 8
devices healthy, and the devices section showed the Floor 2 switch with a status of
down.

## 2. Root cause

The Floor 2 switch was reported down, removing connectivity for everything on that
floor.

Note: the reported symptom was intermittent (a repeating ~30-second drop-and-recover)
rather than a constant outage. The switch status was observed as down; whether the
underlying fault was a hard failure or an intermittent/flapping condition was not
investigated further. The origin of the fault is therefore unconfirmed.

## 3. Action taken

- Isolated the fault to the Floor 2 switch from the scope (wired + wireless, single
  floor).
- Confirmed the switch status as down in the devices section.
- Rebooted the switch; it returned online.
- Asked the user to recheck their connection.
- Posted a resolved/known-issue notice in the general company chat to prevent
  duplicate tickets for the same outage.

## 4. Verification

- Switch returned online after reboot.
- User confirmed connection restored.

## 5. Status

**Resolved (monitor for recurrence)** — connectivity restored via switch reboot.
Given the intermittent nature of the original symptom, the switch should be watched
for the pattern returning, as a reboot may not address an underlying intermittent
fault.

---

## Lessons learned

1. **Wired and wireless failing together on one floor points to the shared switch.**
   The combination rules out an access point (wireless only) and individual devices,
   and the single-floor scope points to that floor's switch rather than a
   building-wide cause.

2. **Confirm the suspected device before acting.** Checking the server room overview
   and the device status turned a hypothesis into a verified fault before any reboot.

3. **An intermittent fault may not be cleared by a reboot.** A repeating
   drop-and-recover can indicate a switch that is failing rather than simply down; a
   reboot restores service but may not resolve an intermittent condition, so the
   device warrants monitoring for recurrence.

4. **Communicate multi-user outages.** A known-issue notice for a shared outage
   prevents duplicate tickets while the fix is applied.
