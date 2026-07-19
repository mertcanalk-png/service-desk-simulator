# Ticket 20 — Company-Wide Internet Slowdown (Core Router Failure)

> Self-directed simulator practice. Fictional data. Not paid work.

| Field | Detail |
|---|---|
| Priority | Critical |
| Category | Network / Infrastructure |
| Reported symptom | Entire office reporting extremely slow internet; pages take 20-30 seconds to load. Internal WAN applications also affected. Speed tests showed roughly 2 Mbps against an expected 500 Mbps. Ongoing all morning. |

---

## 1. Diagnosis

The fault affected the entire office at once, across both internet browsing and
internal WAN applications. An impact at that scale — every user, every service that
depends on the connection — points to a single shared upstream component rather
than individual machines or one segment of the network. For a whole-office
slowdown, that shared component is the core router.

The server room was checked and the core router showed a down/offline status.

## 2. Root cause

The core router had failed and was offline, removing or severely degrading
connectivity for the whole office.

A useful distinguishing check for this class of fault: internet/WAN-bound traffic
being slow while purely internal, LAN-only resources (not leaving the building)
remain fast points specifically at the router, since router and core switch sit at
different points in the path. If internal-only resources were also affected, that
would point at the core switch instead. In this ticket, the affected internal
applications were WAN-dependent, which is consistent with a router-level fault
rather than a contradiction; whether purely LAN-only resources were separately
checked and found unaffected was not confirmed.

A router can degrade in throughput for reasons such as routing table bloat or a
process/memory leak, which a reboot clears — this is a plausible general
explanation for why the reboot resolved the symptom, not a confirmed diagnosis of
this specific device.

Note: the reported speed test result (approximately 2 Mbps) does not fully align
with a device showing as fully offline, since a completely down device would be
expected to show no throughput at all rather than a reduced rate. Whether the
2 Mbps reading was taken before the router's status reached full failure, measured
over a partial path, or reported informally by the user was not established. The
sequence between the degraded speed and the offline status is not fully
reconciled.

## 3. Action taken

- Isolated the fault to the core router based on the office-wide, multi-service
  scope of the impact.
- Checked the server room and confirmed the core router's status as down.
- Rebooted the core router.
- Confirmed the router came back online.

## 4. Verification

- Router returned to an online status after reboot.
- Confirmed with the user that internet access was restored at expected speed.

## 5. Status

**Resolved (cause of the failure unconfirmed)** — connectivity and expected speed
restored after the core router reboot.

---

## Lessons learned

1. **Office-wide, multi-service impact points to a shared upstream device.** When a
   slowdown or outage affects every user and multiple types of service at once, the
   fault is almost always in a component they all pass through, not in individual
   machines.

2. **Distinguish router from core switch by checking LAN-only resources.** If
   internet/WAN-bound traffic is slow but purely internal resources (nothing
   leaving the building) stay fast, the router is the likely bottleneck. If
   internal-only resources are also affected, the fault is more likely the core
   switch. Checking this narrows the diagnosis before acting.

3. **Reconcile the reported symptom with the confirmed status.** A "down" status and
   a non-zero speed reading do not obviously belong to the same moment — noting that
   inconsistency is more useful than silently accepting a status that does not fully
   match the reported numbers.

4. **A restored service does not explain why the core device failed.** The router
   was returned to service, but the reason it went down was not established, so
   recurrence has not been ruled out.
