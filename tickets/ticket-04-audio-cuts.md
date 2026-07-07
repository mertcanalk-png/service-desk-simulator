# Ticket 04 — Audio Cuts Out Mid-Call

> Self-directed simulator practice. Fictional user/data. Not paid work.

| Field | Detail |
|---|---|
| Priority | Medium |
| Category | Software / Network (VoIP) |
| Reported symptom | On softphone calls, audio cuts out intermittently. No constant static — it drops and returns. |

---

## 1. Diagnosis

I updated the headset driver and rebooted, and the problem cleared. That is an
honest account of what happened — but it is **not** a confirmed root cause, and
this ticket is logged partly as a lesson in that distinction.

A clean intermittent drop-out on a VoIP softphone (audio disappears and comes back,
with no persistent crackle) is the classic signature of a **network** issue —
jitter or packet loss — not a hardware/driver fault. Constant static would point at
hardware; clean drop-outs point at the call path.

## 2. Root cause

**Unconfirmed.** The driver update and the reboot were done together, so it's not
possible to say which resolved it — and the reboot alone may have cleared a
transient state. The symptom signature actually pointed more at the network than at
the driver.

## 3. Action taken

- Downloaded and installed the latest headset driver.
- Rebooted the machine.
- Call audio was stable afterwards.

## 4. Verification

- Test call completed with no drop-outs.
- User confirmed calls were working.

## 5. Status

**Resolved (cause unproven)** — working again, but the true cause was not isolated.

---

## Lesson learned

Two lessons, and they're the point of logging this one honestly:

1. **Match the fix to the symptom signature.** Clean mid-call drop-outs on VoIP are
   usually network/jitter/packet-loss, not drivers. My first move should have been
   to isolate the call path, not update a driver.
2. **Change one variable at a time.** Updating the driver *and* rebooting together
   means I can't prove which one helped — "it works now" is not "I found why."
