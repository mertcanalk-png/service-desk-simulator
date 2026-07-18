# Ticket 18 — Laptop Locked at BitLocker Recovery Screen

> Self-directed simulator practice. Fictional data. Not paid work.

| Field | Detail |
|---|---|
| Priority | High (user fully locked out, no access to work files) |
| Category | Security / Device Encryption |
| Reported symptom | Laptop boots to a blue screen requesting a recovery key. User does not have the key and cannot access the device at all. |

---

## 1. Diagnosis

A boot-time screen requesting a recovery key is a BitLocker recovery prompt —
Windows' disk encryption has locked the drive because it detected a condition it
does not trust (common triggers include a firmware/BIOS update, a boot order
change, or a hardware change). The device is unusable until the correct recovery
key for that specific machine is supplied.

## 2. Verification before action

Before any key was retrieved, the user's identity was verified (a verification
code sent and confirmed over chat). The recovery key was then located using the
**specific recovery key ID displayed on the user's blue screen**, matching the key
to that exact device rather than to the user's account generally — a user can have
more than one device, each with its own key, so the key ID is what ties the
recovery key to the correct machine.

## 3. Action taken

In this simulator, the interface allowed the recovery key to be entered directly
into the user's session. This is noted as a simplification of the simulator: in a
production environment, BitLocker recovery occurs before Windows and networking
have loaded, so a technician typically cannot remote into the device at that stage.
The standard method is to read the recovery key to the user by voice, with the user
entering it on their own keyboard, after identity and key-ID verification are
complete.

- Verified identity via a chat-delivered verification code.
- Matched the recovery key to the specific key ID shown on the affected device.
- Entered the recovery key to unlock the device (via the simulator's remote
  session).

## 4. Verification

- Device unlocked and booted into Windows successfully.
- User confirmed access to the device and work files restored.

## 5. Status

**Resolved** — correct recovery key applied to the matched device; access restored.

---

## Lessons learned

1. **Match the recovery key to the device's key ID, not just the user's account.**
   A user can have multiple devices, each with a distinct BitLocker key — the key ID
   shown on the recovery screen is what confirms the correct key for that specific
   machine.

2. **BitLocker recovery happens pre-boot, before networking is available.** In a
   production environment a technician cannot typically remote into a device at the
   recovery screen; the standard method is to verify identity and key ID, then read
   the key aloud for the user to enter themselves. The simulator's direct-entry flow
   does not reflect this constraint.

3. **Identity verification precedes releasing any recovery key.** A disk recovery
   key grants full access to an entire encrypted drive, making identity
   verification before release non-negotiable.
