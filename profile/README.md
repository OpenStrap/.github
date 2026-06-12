![OpenStrap](https://raw.githubusercontent.com/OpenStrap/.github/main/profile/banner.png)

# OpenStrap

Your WHOOP band doesn't stop working when the subscription does — the app just goes
dark. OpenStrap is what I built so a 4.0 band that would otherwise sit in a drawer keeps
doing something: read your own data off it over Bluetooth, keep the raw bytes, and turn
them into the numbers you actually look at.

Is it a replacement for WHOOP? No, and I'm not going to pretend it is. They've got years
of research and a whole team; this is one person and textbook methods. But it's a real
second life for hardware you already own, and your data stays yours.

Tested on WHOOP 4.0 only. Once you start using it, don't reconnect the band to the
official WHOOP app — a firmware update could change or break the events this relies on.

### The pieces

- **[edge](https://github.com/OpenStrap/edge)** — the phone app. Connects to the band,
  drains it, shows your day. [Download the APK →](https://github.com/OpenStrap/edge/releases)
- **[backend](https://github.com/OpenStrap/backend)** — the server. Ingests raw frames
  and computes everything. One Cloudflare Worker; self-host it or use mine.
- **[analytics](https://github.com/OpenStrap/analytics)** — the math. Published methods
  (Banister TRIMP, Cole-Kripke, and friends) turn heart rate and motion into metrics.
- **[protocol](https://github.com/OpenStrap/protocol)** — the decoders. Raw WHOOP 4.0
  record bytes into named fields.
- **[research](https://github.com/OpenStrap/research)** — the protocol reference, plus a
  client to talk to a band yourself.

### A few honest notes

There are bugs. Please open issues as you find them and I'll work through them. A lot of
the protocol — the events especially — is empirical guesswork, and no one person can
confirm it to 100%. The more people poke at it, the closer we get to nailing every field
down with real confidence.

Not affiliated with, endorsed by, or connected to WHOOP. MIT licensed.
