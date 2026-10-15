# Ghostly runtime config

`gsa.json` decides how Ghostly talks to Apple's sign-in service (desktop 1.5.3+, iPhone 1.3.3+).
Apple changes what it accepts without warning, so these values are published here: edit, push,
and clients use the new values on their next sign-in. GitHub's raw cache can serve the old file
for up to 5 minutes. No release needed.

| Field | What it is | Rules the apps enforce |
|---|---|---|
| `client_info` | `X-MMe-Client-Info` on every sign-in request | printable ASCII, starts with `<`, at most 200 characters |
| `anisette_servers` | anisette v3 servers, tried in order | at most 2, `https://` only. Their ADI library must match the OS in `client_info` (check `<server>/v3/client_info`) |
| `headers` | extra or replacement headers on every sign-in request | at most 8; `User-Agent` or `X-` names only; never `X-Apple-Identity-Token` or `X-MMe-Client-Info` |

If any field breaks a rule, or the file can't be fetched, the app ignores the whole file and uses
its built-in values (the same as this file on 2026-10-15). Apple's own URLs never come from here.

Before pushing a change, check it with a made-up account:
`GHOSTLY_GSA_PROFILE_URL=http://127.0.0.1:<port>/gsa.json ghostly-sideload login` against a local copy.
`authentication-20970` means Apple reached the account check. `unknown-plist-503` means it refused the
client. Only a real account reaches the post-password checks (-27952 "Update iCloud for Windows" was one).
Reports show what a client used in its `gsa_profile=` log line.
