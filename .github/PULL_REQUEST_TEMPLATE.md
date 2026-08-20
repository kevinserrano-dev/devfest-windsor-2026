## What does this change?

<!-- A sentence or two, the way you'd want to read it in a changelog. -->

## Why?

<!-- The problem behind it. Link the issue or discussion if there is one. -->

## Type of change

- [ ] Bug fix
- [ ] New feature
- [ ] Breaking change
- [ ] Refactor / internal
- [ ] Documentation

## Screenshots

<!-- Needed for anything visible. Before/after side by side if it's a change to existing UI. -->

## Checklist

- [ ] Ran `build_runner` after touching annotations
- [ ] `flutter analyze --fatal-infos` clean, `dart format .` applied, `custom_lint` passing
- [ ] `flutter test` passing
- [ ] Nothing in `features/` imports Firebase, drift or `http`
- [ ] No hardcoded color, spacing, radius, duration or font
- [ ] No literal user-facing strings, everything through `l10n`
- [ ] Repository errors come back as `Result` / `AppFailure`
- [ ] Navigation uses typed routes, and nothing navigates imperatively on an auth state change
- [ ] Anything newly persisted per user has a `SessionCleaner` and a `uid`-namespaced key
- [ ] No secrets, keys, `google-services.json` or `GoogleService-Info.plist` committed
