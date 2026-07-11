# Nontact

**The no-maintenance address book.** Nobody maintains contact data about
anyone else.

Everyone keeps their own encrypted, authoritative contact record and grants
scoped access to it. Your "address book" is not a pile of copies you have to
keep fresh — it's a set of capabilities (a pointer plus a decryption right)
that always dereference to the other person's *current* data. N
self-maintained records instead of N² rotting copies.

- **Live update** — edit a field, republish; every grantee sees the new value
  on their next fetch. Nobody re-sends a vCard.
- **Real revocation** — unshare rotates the scope key; revoked parties keep
  what they already decrypted (honest, physical-world semantics) but see
  nothing new and their view is marked stale.
- **Scoped** — share a "basic" card with acquaintances and a "personal" card
  with friends; the two are separate encrypted scopes under one identity.
- **Recoverable** — your whole graph rebuilds from your nsec alone; the
  encrypted Grant Index (kind 10440) is the only state.
- **No server, no accounts, no build step.** Relays store only ciphertext and
  never learn who shares what with whom.

Built on draft **NIP-DA** Scoped Data Grants
([review pending](https://github.com/nostr-protocol/nips/pull/2411);
spec + reference lib at
[nostr-scoped-data-grants](https://github.com/JAFairweather/nostr-scoped-data-grants)).
Kind numbers may change — use throwaway keys and treat data as ephemeral.

## Run it

```
npm install
npm run web    # http://localhost:4444/
npm run seed   # publishes a throwaway demo graph to live relays, prints an nsec to sign in with
```

Sign in with a NIP-07 extension, paste a throwaway nsec, or generate one in
the tab. `npm run seed` prints a pre-populated demo identity and a cheat sheet
for the live-update walkthrough.

Pure client: `index.html` + `app.mjs`, no framework, no bundler. `lib/` is
vendored from the protocol repo (`npm run sync-lib` refreshes it); `nipxx.mjs`
is isomorphic, so the browser runs the same protocol library as Node.

## One of four NIP-DA apps

Nontact is part of a family of independent apps built on NIP-DA Scoped Data
Grants:

- **[Nontact](https://github.com/JAFairweather/nontact)** — the no-maintenance
  address book (this repo).
- **[Nvelope](https://github.com/JAFairweather/nvelope)** — live folders, real
  revocation (encrypted document sharing).
- **[Notegate](https://github.com/JAFairweather/notegate)** — serverless
  secure tip intake.
- **[Nvoy](https://github.com/JAFairweather/nvoy)** — scoped, revocable data
  delegation to AI agents (MCP server).

MIT.
