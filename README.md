<div align="center">

# DevFest Windsor 2026

**The official mobile app for DevFest Windsor 2026.**

[![CI](https://github.com/kevinserrano-dev/devfest-windsor-2026/actions/workflows/ci.yml/badge.svg)](https://github.com/kevinserrano-dev/devfest-windsor-2026/actions/workflows/ci.yml)
[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)
[![Flutter](https://img.shields.io/badge/Flutter-3.47-02569B?logo=flutter&logoColor=white)](https://flutter.dev)
[![PRs welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](CONTRIBUTING.md)

</div>

## What is this

A Flutter app for people attending DevFest Windsor 2026: schedule, sessions, speakers, venue, and reminders.

It follows the Flutter team's [architecture guidance](https://docs.flutter.dev/app-architecture). PR rules are in [CONTRIBUTING.md](CONTRIBUTING.md).

## What's in it

- Offline-first. SQLite (via [drift](https://drift.simonbinder.eu/)) is the source of truth; Firestore feeds it. The app works with no network.
- Local notifications that survive reboots, timezone changes, and DST.
- Auth-guarded navigation with go_router.
- A token-based design system. Changing one file rebrands the app.
- Firebase: Auth, Firestore, Remote Config, Analytics, Crashlytics, Messaging, App Check.

## Stack

| Area | Choice |
|---|---|
| Architecture | MVVM + feature-first (UI / Data layers) |
| State & DI | Riverpod 3 (`@riverpod` codegen) |
| Navigation | go_router (typed routes) |
| Local database | drift (SQLite) |
| Models | freezed + json_serializable |
| Notifications | flutter_local_notifications + timezone |
| Backend | Firebase |
| Tests | flutter_test + mocktail |

## Running it

```bash
git clone https://github.com/kevinserrano-dev/devfest-windsor-2026.git
cd devfest-windsor-2026

flutter pub get
dart run build_runner build --delete-conflicting-outputs
flutter run
```

Needs Flutter 3.47.0+ on stable, Dart 3.13+, and either your own Firebase project or the emulator. [CONTRIBUTING.md](CONTRIBUTING.md) covers both, including working without a Firebase project.

## Project structure

```
lib/
├── bootstrap.dart
├── core/                 # design system, router, database, notifications, firebase, errors
├── features/<name>/
│   ├── data/             # dtos, datasources, repository impls
│   ├── domain/           # entities, repository interfaces
│   └── presentation/     # routes, view_models, screens, widgets
└── l10n/
```

## Contributing

See [CONTRIBUTING.md](CONTRIBUTING.md) and [good first issue](https://github.com/kevinserrano-dev/devfest-windsor-2026/labels/good%20first%20issue).

[Code of Conduct](CODE_OF_CONDUCT.md). Security reports go through [private disclosure](SECURITY.md) — don't open a public issue for those.

## Maintainer

[Kevin Serrano](https://github.com/kevinserrano-dev), for the Windsor developer community.

## License

[MIT](LICENSE) © 2026 Kevin Serrano