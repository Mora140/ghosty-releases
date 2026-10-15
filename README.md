# Ghostly runtime config

`gsa.json` holds the `X-MMe-Client-Info` value Ghostly sends on every Apple sign-in request
(desktop 1.5.3+, iPhone 1.3.3+). Apple changes which value it accepts without warning, so it is
published here: edit `client_info`, push, and clients pick it up on their next sign-in (GitHub's
raw cache holds the old file for up to 5 minutes). No release needed.

Rules the apps enforce: `client_info` is printable ASCII, starts with `<`, at most 200 characters.
Anything else, or this file being unreachable, makes the app use its built-in value. Only this
header value is read; URLs never come from here.

Check a value before pushing it: the credential-free probe in the Ghosty repo's
`apple-gsa-80045-client-os` notes, or
`GHOSTLY_GSA_PROFILE_URL=<local copy> ghostly-sideload login` with a made-up account
(`authentication-20970` = Apple reached the account check, `unknown-plist-503` = refused).
