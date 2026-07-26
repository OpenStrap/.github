# Security Policy

Org-wide default. [protocol][p], [analytics][a] and [edge][e] each have their own
`SECURITY.md`, which overrides this for those repos.

## Reporting a vulnerability

Please **don't** open a public issue for a security problem.

Use GitHub's private vulnerability reporting on the affected repo — the
**Security** tab → **Report a vulnerability**. That reaches the maintainer and
stays private until there's a fix.

Honest expectations, since this is a one-maintainer project rather than a company
with an on-call rota:

- Acknowledgement within about a week.
- An assessment, and a fix or a clear "won't fix, and here's why", within 30 days
  for anything that puts user data at risk.
- Credit in the release notes if you'd like it.

## Where the data actually is

Worth knowing before you go looking, because it determines what's worth
reporting: OpenStrap computes and stores health data **on the phone**. There's no
account and no server holding it. Two qualifications, so the boundary is exact:

- **Anonymous diagnostics** (Firebase crash/performance — never health data) are
  **on by default in GitHub release builds**, switchable off in-app, and absent
  entirely from App Store / Play Store builds.
- **Health-data contribution** does upload the local database, but is opt-in, off
  by default, and compiled out of store builds.
- The **BYOK AI assistant**, if you configure one, sends your metrics to
  whichever provider you chose, under their policies.

So the realistic attack surface is the phone, the Bluetooth link, and the local
database — not a cloud backend. Reports focused there are the most useful.

## In scope

- Anything that discloses a user's health data off their device.
- Anything letting a third party read, write to, or hijack the Bluetooth session
  with a band.
- Local data-at-rest problems: the database, exports, the iOS App Group
  container, widget snapshots.
- The optional companion worker: auth, import endpoints, the opt-in telemetry and
  health-upload paths.
- Anything causing data to go somewhere the user didn't agree to.

## Out of scope

- **The band's firmware.** We don't ship it, can't patch it, and won't publish
  attacks against it.
- **WHOOP's own apps and services.** Please report those to WHOOP.
- Sideloaded builds being unsigned, or a rooted/jailbroken device reading app
  storage. Both are known properties of the distribution model and documented.
- Metric accuracy. Wrong numbers are bugs — open a normal issue.

[p]: https://github.com/OpenStrap/protocol
[a]: https://github.com/OpenStrap/analytics
[e]: https://github.com/OpenStrap/edge
