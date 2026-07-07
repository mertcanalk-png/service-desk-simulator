# Ticket 06 — VPN Won't Reconnect

> Self-directed simulator practice. Fictional user/data. Not paid work.

| Field | Detail |
|---|---|
| Priority | Medium |
| Category | Network / Access |
| Reported symptom | Working from home; VPN won't reconnect. |

---

## 1. Diagnosis

I ran `ipconfig /flushdns` and rebooted, and the VPN came back. As with Ticket 04,
that's an honest account of what worked — but the two changes were made together, so
the true cause is unproven, and this ticket is logged partly to correct my own
wording about *what the tool actually does*.

## 2. Root cause

**Unconfirmed.** The reboot (which restarts the VPN client and network adapter and
clears transient state) is the more likely fix; the flushdns may have been
incidental.

Important precision — what `ipconfig /flushdns` actually does:

- It **clears the DNS resolver cache** (stored name-to-IP lookups).
- It does **not** renew IP addresses — that's DHCP (`ipconfig /release` +
  `/renew`).
- There is no "VPN cache" being cleared.

## 3. Action taken

- Ran `ipconfig /flushdns`.
- Rebooted the machine.
- VPN reconnected afterwards.

## 4. Verification

- VPN established a connection after the reboot.
- User confirmed they were back online.

## 5. Status

**Resolved (cause unproven)** — working again, cause not isolated.

---

## Lesson learned

1. **Name a tool's real function accurately.** `flushdns` clears the DNS resolver
   cache — not IP addresses, not a "VPN cache." Getting this right in notes is the
   difference between understanding the fix and guessing.
2. **Change one variable at a time.** flushdns *then test*, reboot only if still
   failing — otherwise the cause stays unproven.
