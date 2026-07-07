# Ticket 03 — Password Expired After a Long Absence

> Self-directed simulator practice. Fictional user/data. Not paid work.

| Field | Detail |
|---|---|
| Priority | Medium |
| Category | Identity / Access |
| Reported symptom | Back from three weeks' leave; password no longer works. |

---

## 1. Diagnosis

The pattern — credentials that worked before an absence and stopped during it —
strongly suggests a password that expired on schedule while the user was away,
rather than a compromise or a locked account. But before doing anything to the
account, identity has to be confirmed.

I ran identity verification first (out-of-band code / read-back), because a
"reset my password" request is exactly the shape a social-engineering attempt
takes, and this was a higher-value account under time pressure.

## 2. Root cause

The password had expired during the three-week absence. This is a routine,
expected outcome of a password-age policy — not an indicator of anything
malicious.

## 3. Action taken

- Verified the user's identity before touching the account.
- Reset the password with a **temporary password + "must change at next logon."**

## 4. Verification

- User logged in with the temporary password and was prompted to set their own.
- After setting a new password, normal access resumed.

## 5. Status

**Resolved** — identity verified, password reset with forced change on first login.

---

## Lesson learned

**Verify identity before any account or security action — it's mandatory, not
optional.** And distinguish account states precisely: *expired* is not *locked* is
not *disabled*. This was expired-after-absence, which is routine. The temp-password-
plus-force-change pattern is the clean way to hand back access without the
technician ever knowing the user's real password.
