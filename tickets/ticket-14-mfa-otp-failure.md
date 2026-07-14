# Ticket 14 — Cannot Log In: MFA Code Not Arriving

> Self-directed simulator practice. Fictional data. Not paid work.

| Field | Detail |
|---|---|
| Priority | High (project deadline; user locked out of all company systems) |
| Category | Identity / MFA |
| Reported symptom | User cannot complete login — the OTP code is not arriving at the registered phone number. Restarting the phone and repeated login attempts did not help. |

---

## 1. Diagnosis

The username and password stage of login was succeeding — the system was reaching
the point of sending the OTP. The failing component was therefore the second
factor (MFA delivery), not the credentials. The issue was isolated to the user's
registered MFA method failing to deliver codes.

## 2. Root cause

The registered MFA method was not delivering codes to the user's verified phone.

Note: the specific origin of the delivery failure (carrier delivery issue,
authenticator time drift, or a corrupted enrolment) was not separately isolated.
Re-enrolling the MFA method restored access. A password reset was also performed in
the same fix, so the resolving change is not singly isolated.

## 3. Action taken

- Notified the user's manager that an MFA reset was required — a second-party
  check, since MFA resets are a common social-engineering target.
- Verified the user's identity before any account change.
- Reset the user's MFA enrolment, generating a new QR code for the user to
  re-register their authenticator at next login.
- Issued a temporary password with change-at-next-logon and provided it to the
  user.

## 4. Verification

- User re-enrolled MFA and completed login successfully.
- User confirmed access to company systems restored.

## 5. Status

**Resolved** — MFA re-enrolment restored login.

---

## Lessons learned

1. **Identify which factor is failing before acting.** Credentials succeeding but
   the OTP not arriving isolates the fault to the second factor — the fix targets
   MFA enrolment, not the password.

2. **The password reset was not required.** The password was functioning; resetting
   it changed a second variable in the same fix, leaving the resolving action
   unproven and expanding the change beyond the fault. The smallest fix matching
   the fault was the MFA re-enrolment alone.

3. **Never deliver credentials over chat.** A temporary password sent in a chat
   message persists in history as plain text. Credentials should be delivered
   verbally on a call or via a secure one-time link, always paired with
   change-at-next-logon.

4. **Manager notification is a sound control on MFA resets.** Because MFA resets
   are a known social-engineering vector, a second-party notification or approval
   adds a check beyond identity verification alone.
