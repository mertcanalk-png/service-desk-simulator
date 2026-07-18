# Ticket 17 — Remote User's WiFi Not Connecting (Home Network)

> Self-directed simulator practice. Fictional data. Not paid work.

| Field | Detail |
|---|---|
| Priority | Medium |
| Category | Network / Remote Connectivity |
| Reported symptom | Remote worker's WiFi will not connect; no other users are affected. Toggling WiFi off/on and restarting the computer did not resolve it. |

---

## 1. Diagnosis

The user is a remote worker, so "everyone else is fine" does not point at company
infrastructure — she is not on it. With only her device affected, and the fault
tied to her connection specifically, the issue is scoped to her home network
profile stored on her laptop rather than a shared cause.

## 2. Root cause

The laptop's saved WiFi profile for the home network no longer matched what the
router expected, preventing a successful connection.

Note: the specific origin (a changed router password, a mismatched saved key, or a
stale cached profile) was not separately isolated. Forgetting the network and
reconnecting with the current key resolves any of these in the same way, so the
precise cause is not distinguished by the fix.

## 3. Action taken

- Connected to the user's machine via remote support.
- Removed ("forgot") the saved home WiFi network profile on the laptop.
- Reconnected using the current WiFi key, entered fresh rather than relying on the
  cached credential.

## 4. Verification

- Connection established successfully with the fresh profile.
- User confirmed WiFi was working normally.

## 5. Status

**Resolved (specific cause unconfirmed)** — connectivity restored via a fresh WiFi
profile using the current key.

---

## Lessons learned

1. **For a remote worker, "only one user affected" points at their home network,
   not company infrastructure.** Scope reasoning still applies, but the shared
   dependency to isolate is the user's own environment, not a company access point
   or switch.

2. **A fix that works does not confirm which specific cause was present.**
   Forgetting and reconnecting a WiFi profile resolves a stale cache, a mismatched
   key, or a changed router password identically — the fix does not distinguish
   between them, so the cause should be recorded as unconfirmed rather than named
   outright.

3. **Confirm the environment before naming the fault.** Establishing that the
   affected network was the user's home WiFi, not a company-managed profile,
   changes what the ticket is actually about and keeps the diagnosis accurate to
   the real setup.
