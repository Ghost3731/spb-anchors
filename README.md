# Seremaci Prestige Bank: anchor archive

Public copy of the signed "anchors" of the Seremaci Prestige Bank (a B2B seller-bank core, work in progress, not live, no customer money).

Each `anchor-NNNNNN.json` is a signed snapshot of the newest hash of each of the bank's hash chains (ledger, audit log, end-of-day reports, payment events).
Anchors are numbered, and each one contains the SHA-256 of the file before it, so removing or inserting one is detectable. Files are only ever added, never changed.
Their purpose: anyone can later check that the bank's history was not rewritten, cut off, or replaced by an older backup.

## The signing key

- Algorithm: Ed25519
- Public key: `anchor.key.pub` (PEM, in this repository)
- **Fingerprint (key_id): `4bd8328a0c35b3899921c971317b71fbea3602940887ae99272440efc8373701`**
  = SHA-256 of the public key in DER (SPKI) form. It is also written in every anchor as `key_id`.

Check that the file `anchor.key.pub` is the key named above:

    openssl pkey -pubin -in anchor.key.pub -outform DER | shasum -a 256

The result must be exactly the fingerprint above. Compare against this text, never only against the key file next to it.
Fingerprint first published: 2026-11-16. If the key is ever replaced, the new fingerprint and the date are added here, and the old one stays listed.

## Rules for this repository

- Only new anchor files and, once, the public key are added. History is never rewritten (branch protection: no force-push, no branch deletion).
- A missing anchor, a file that differs from what the bank holds, or a key that differs from the fingerprint above is an alarm.
