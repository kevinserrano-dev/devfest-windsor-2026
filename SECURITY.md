# Security Policy

## Supported versions

| Version | Supported |
|---|---|
| Latest release | yes |
| `master` | yes |
| Older releases | no, please update |

This is a mobile app rather than a library, so the only version I can realistically fix is the
current one.

## Reporting a vulnerability

Please don't open a public issue.

Use GitHub's private reporting instead:
[**Report a vulnerability**](https://github.com/kevinserrano-dev/devfest-windsor-2026/security/advisories/new).
It opens a private thread and lets me credit you in the advisory once it's published. If that form
isn't available to you, email kevin.serrano.mojica@gmail.com.

Helpful to include:

- What the issue is and what someone could actually do with it.
- Steps to reproduce, or a proof of concept.
- The version or commit you tested.
- Whether it's public anywhere already.

What to expect:

| | Target |
|---|---|
| Acknowledgement | 72 hours |
| Initial assessment | 7 days |
| Fix or mitigation plan | 30 days for anything exploitable |

I'll keep you updated, and I won't publish an advisory naming you without asking first.

## Scope

In scope:

- The Flutter app in this repository.
- Firestore security rules, including any rule that lets one user read or write another user's data.
- Anything here that leaks credentials, tokens or personal data.
- Auth and session handling: bypassing the guard, session fixation, data surviving a sign-out.

Out of scope:

- Google and Firebase infrastructure itself. Those go to [Google VRP](https://bughunters.google.com/).
- Issues needing a rooted or jailbroken device plus physical access, unless they expose someone
  else's data.
- Social engineering of maintainers or event organizers.
- Missing hardening that isn't exploitable on its own, like "no certificate pinning". Those are
  welcome as regular issues.

## A note for contributors

This repo is public, so anyone can read exactly how the client works. That's fine and intentional:
security lives in the Firestore rules and in App Check, never in the client. If you catch yourself
writing a check that only holds because an attacker can't see the code, that's the bug.

Never commit `google-services.json`, `GoogleService-Info.plist`, signing keys or `.env` files.
They're gitignored, and if you find one that isn't, that's a valid report.
