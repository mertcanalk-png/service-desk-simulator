# Ticket 12 — Cloud Drive Errors and Duplicating Files

> Self-directed simulator practice. Fictional data. Not paid work.

| Field | Detail |
|---|---|
| Priority | Medium |
| Category | Software / Cloud (with a security consideration) |
| Reported symptom | Cloud Drive showing errors and files duplicating continuously. User reported recently installing unauthorised free software (a screen-saver downloaded from the internet) shortly before the problem began. |

---

## 1. Diagnosis

The immediate symptom was Cloud Drive sync errors with files duplicating. Continuous
duplication of this kind is consistent with sync conflicts — files reconciled in
more than one location before syncing completed.

The reported sequence is relevant: the problem began shortly after the user
installed unauthorised software from the internet. That timing makes the
unauthorised software a likely contributor (for example a second, unofficial client
or process interacting with the same files), and — independent of the sync issue —
untrusted internet-sourced software on a company machine is a security exposure in
its own right.

## 2. Action taken

- Connected to the user's PC via Remote Support.
- Opened Cloud Drive and forced a resync to reconcile file versions and clear the
  conflicts.
- Confirmed in File Explorer that the files were synced correctly.

## 3. Verification

- Sync errors cleared and duplicate conflicts resolved after the resync.
- Files confirmed synced correctly.

## 4. Status

**Resolved (immediate issue)** — sync conflicts cleared and files reconciled.

Note: the resync addressed the current conflicts but did not remove the unauthorised
software that preceded the problem. If that software is the cause, the duplication
can recur; and separate from the sync issue, unauthorised internet-sourced software
on a company machine is an outstanding security item. Removal of the software and a
malware scan are the appropriate follow-up, per policy.

---

## Lessons learned

1. **Clearing the symptom is not the same as removing the cause.** A forced resync
   reconciles the current conflicts, but if an installed program is generating the
   duplication, the conflicts can return until that program is removed. Confirming
   the problem stays resolved requires addressing what triggered it.

2. **Unauthorised software is a security item, not just a functional one.** Software
   downloaded from the internet onto a company machine is a common malware vector and
   a policy concern regardless of whether it caused the reported fault. It warrants
   removal and a malware scan, and a flag to the appropriate team where policy
   requires.

3. **Weight the details the user volunteers.** The user naming a recent unauthorised
   install is a direct pointer to a likely cause; the reported timeline should shape
   the diagnosis rather than be set aside once the visible symptom is cleared.
