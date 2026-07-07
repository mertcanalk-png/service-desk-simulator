# Ticket 05 — Email Won't Set Up on a New Phone

> Self-directed simulator practice. Fictional user/data. Not paid work.

| Field | Detail |
|---|---|
| Priority | Medium |
| Category | Email / Identity |
| Reported symptom | Can't set up company email on a new phone — "cannot connect to server." |

---

## 1. Diagnosis

"Cannot connect to server" on a phone looks like a mail-server or device-config
problem, but the knowledge-base runbook's first step is an **isolation question**:
can the user access email anywhere else — webmail or their workstation?

I asked, and email was **also failing on the workstation**. That single answer
changes everything: if it failed only on the new phone, it would be a device/config
issue; failing on a known-good device too means the problem is with the account,
not the phone. That routed the ticket to the account/password branch.

## 2. Root cause

A **password issue** on the account (expired/needs reset). Note the precise wording:
this was a password state, **not** "account disabled" — those are distinct states,
and the note should say exactly which one it was.

## 3. Action taken

- Applied the runbook isolation step (checked access on another device).
- Verified the user's identity.
- Reset the password with a temporary password + force-change at next logon.

## 4. Verification

- User signed in with the new password.
- Email synced on both the workstation and the new phone.

## 5. Status

**Resolved** — password reset; email working on both devices.

---

## Lesson learned

**Isolate scope before you fix.** One question — "does it fail on your other
device too?" — instantly separated a device problem from an account problem and
sent the ticket down the right branch. And **match note wording to the actual
account state**: "password issue" and "account disabled" are not interchangeable.
