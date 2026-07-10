# Ticket 11 — Suspected Account Compromise (Escalated)

> Self-directed simulator practice. Fictional data. Not paid work.

| Field | Detail |
|---|---|
| Priority | Critical (suspected security breach; account handles sensitive financial data) |
| Category | Security / Identity |
| Reported symptom | User received an alert of a sign-in from an unfamiliar location they do not recognise and did not perform. User had already changed their own password before contacting support. |

---

## 1. Diagnosis

An alert of a sign-in from a location the user does not recognise, on an account
handling sensitive financial data, is treated as a suspected account compromise.
The user had already changed their password from their own session — but a password
set from a potentially compromised state cannot be trusted, and a password change
alone does not address session tokens or MFA that an attacker may already hold. The
ticket is therefore handled as a containment case, not a simple password reset.

## 2. Containment actions taken

Actions were taken in order, identity verified first:

- **Verified the user's identity** (out-of-band code, confirmed by read-back)
  before making any change to the account.
- **Reset the password** from a known-clean path with force-change at next logon,
  rather than relying on the reset the user performed from a possibly compromised
  session.
- **Reset MFA**, because an attacker with an existing session or token could
  otherwise retain access despite a password change.
- **Ran a full malware scan** on the user's device via remote access to check for
  malware that could have exposed the credentials.

## 3. Escalation

- **Escalated to the security team** for further investigation. A suspected breach
  on an account with access to sensitive financial data is beyond first-line scope
  and requires security review of the sign-in activity and any exposure.

## 4. Status

**Escalated (open)** — containment actions completed; ticket handed to the security
team for investigation. Not closed.

---

## Lessons learned

1. **Verify identity before acting, even under breach urgency.** The pressure of a
   suspected compromise does not remove the identity-verification step; it makes it
   more important.

2. **A password change is not containment on its own.** MFA reset and session/token
   invalidation matter because an attacker may already hold a valid session — reset
   the password *and* the MFA, and don't trust a password set from a possibly
   compromised session.

3. **Know the limit of first-line scope.** A suspected breach on a sensitive account
   is escalated to security, not closed at L1. Escalation with full context is the
   correct outcome, not an incomplete one.
