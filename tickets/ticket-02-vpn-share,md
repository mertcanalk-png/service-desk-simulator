# Ticket 02 — Remote User Can't Reach a Shared Drive

> Self-directed simulator practice. Fictional user/data. Not paid work.

| Field | Detail |
|---|---|
| Priority | Medium |
| Category | Network / Access |
| Reported symptom | Working from home, can't open the Marketing shared drive — "network path not found." Internet and email work fine. |

---

## 1. Diagnosis

The key detail is what *still worked*: the user had a functioning internet
connection and could send/receive email. That rules out a total connectivity
failure and points at something specific to the internal file share.

I checked whether the user was on the corporate network. They were at home, and
the VPN client was **not connected**. An on-prem file share (`\\FILESERV01\...`)
is only reachable from inside the corporate network, so a working-internet-but-no-
internal-resources pattern is the classic signature of a missing VPN tunnel.

## 2. Root cause

The user was off the corporate network with no active VPN connection. The file
server was never unreachable *in general* — it was unreachable *to them* because
they had no tunnel into the network where it lives.

## 3. Action taken

- Connected via Remote Desktop to assist.
- Started the VPN client and established the tunnel.
- Verified the share path was now reachable.
- Remapped the Marketing drive so it reconnects cleanly next time.

## 4. Verification

- With the VPN connected, the share path resolves and opens.
- Mapped drive reconnects and the user can open their files.
- User confirmed access restored.

## 5. Status

**Resolved** — VPN connected, share verified, drive remapped.

---

## Lesson learned

**"Network path not found" for a remote user who has working internet is a VPN
problem, not a permissions problem.** The instinct is to check share permissions or
suspect the file server, but the tell is that everything internet-facing works
while everything internal fails. That split means the user simply isn't *inside*
the network yet.
