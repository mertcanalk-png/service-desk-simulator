# Ticket 09 — Department Transfer (Access Modification)

> Self-directed simulator practice. Fictional data. Not paid work.

| Field | Detail |
|---|---|
| Priority | High (access required for new role on Friday morning) |
| Type | Service Request — access modification |
| Category | Identity / Access |
| Request | Update a transferring employee's group access: grant new-role access, revoke previous-department access. |

---

## 1. Request detail

An employee (`kpatel`) is transferring from Engineering to IT Infrastructure. The
request requires the new role's tool access to be granted and the previous
Engineering access to be revoked per security policy. Department and reporting-line
changes are handled separately by HR.

## 2. Action taken

- Removed the account from the **Engineering** group.
- Added the account to the **IT Infrastructure** group for the new role.

## 3. Verification

- Confirmed the Engineering membership was removed.
- Confirmed the IT Infrastructure membership was present.
- Access aligned to the new role ahead of the start deadline.

## 4. Status

**Resolved (request fulfilled)** — previous access revoked, new access granted and
verified.

---

## Lessons learned

1. **Revoking old access is as important as granting new access.** On a transfer,
   removing the previous department's group is the security-critical step. Access
   left in place after a role change is access creep and a common audit finding —
   the goal is that permissions match the current role, nothing more (least
   privilege).

2. **A transfer is a request, not an incident.** There is no fault to diagnose; the
   measure of success is that group membership matches the new role and the old
   membership is gone.

3. **Confirm both halves.** Verify the removal and the addition, rather than
   assuming the change applied — a half-completed transfer either blocks the new
   role or leaves stale access behind.
