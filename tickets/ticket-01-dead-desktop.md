# Ticket 01 — Dead Desktop (Replace, Don't Repair)

> Self-directed simulator practice. Fictional user/data. Not paid work.

| Field | Detail |
|---|---|
| Priority | High (user fully unable to work) |
| Category | Hardware — desktop |
| Reported symptom | Desktop won't turn on — no power, no display |

---

## 1. Diagnosis

The user reported the machine was completely dead. Before assuming hardware
failure, I isolated the possible causes in order:

- **Power source?** Moved the machine to a **known-good outlet** to rule out a
  dead wall socket or faulty power lead. Still no power.
- **Does it POST?** With confirmed power available, the unit showed no signs of
  starting — no fans, no POST beep, no display.

With a known-good outlet ruled in and still no POST, the fault is internal to the
machine (power supply or board), not the environment.

## 2. Root cause

Confirmed hardware failure. The unit is dead on a known-good outlet and does not
POST — this is beyond a Level 1 repair and the machine needs replacement, not
troubleshooting.

## 3. Action taken

- Provisioned a replacement unit through the **imaging server (PXE boot)**, which
  applies the standard build and joins the machine to the domain automatically via
  the task sequence.
- Chose the imaging-server build (rather than a cloud-only setup) because this
  user's role depends on a legacy softphone and on-prem policies that the standard
  image includes.
- Verified the replacement by logging in with a domain account and confirming the
  expected applications and policies were present.

## 4. Verification

- Replacement unit powers on, completes POST, and boots the standard image.
- Domain login succeeds; user's applications and mapped resources are present.
- User confirmed they can work again.

## 5. Status

**Resolved** — dead unit replaced, replacement imaged and domain-joined, user back
to work. Faulty unit tagged for return.

---

## Lesson learned

**Confirm dead on a known-good outlet before declaring hardware failure.** The
fastest way to look unprofessional is to condemn a machine that was plugged into a
dead socket. Once genuine failure is confirmed and the unit won't POST, the correct
call is replace, not repair — Level 1 doesn't rebuild power supplies, it restores
the user to working as fast as possible.

*A note on credentials:* the imaging process uses a locked-down deploy account and
the domain join is automated by the task sequence — no passwords are recorded in
ticket notes.
