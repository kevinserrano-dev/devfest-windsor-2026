Contributing
Contributions of any size are welcome, including typo fixes.

Two things this repo is strict about:

Architecture. MVVM, feature-first, Riverpod, following Flutter's official guidance. A PR that ignores the rules gets review comments, not a merge.

Tests. Unit tests on critical code only. No widget, golden, or integration tests. Don't add them.

If this file is wrong or unclear, open an issue.

Quick start
bash
git clone https://github.com/kevinserrano-dev/devfest-windsor-2026.git
cd devfest-windsor-2026

flutter --version            # 3.47.0+, stable
flutter pub get
dart run build_runner build --delete-conflicting-outputs
flutter run
Keep codegen running while you work:

bash
dart run build_runner watch -d
Firebase
Config files are not in the repo. Two options:

Your own free Firebase project (fastest for most work):

bash
dart pub global activate flutterfire_cli
flutterfire configure
Emulator. Copy the .example config files and run firebase emulators:start. Auth, Firestore, and Remote Config work offline that way.

If you can't test something locally, say so in the PR.

Never commit google-services.json, GoogleService-Info.plist, signing keys, or .env files.

Workflow
Open an issue first unless it's a small fix. Claim work there so it isn't done twice. New to the repo? Look for good first issue.

Branch from develop, not master:

text
feat/session-reminders
fix/schedule-tab-resets
docs/contributing-setup
refactor/reminder-repository
chore/bump-riverpod
Conventional Commits — they drive the changelog:

text
feat(reminders): schedule a notification every N days
fix(router): keep the navigation stack when the auth token refreshes
docs(readme): add emulator setup
refactor(auth): extract claim parsing from the repository
chore(deps): bump go_router to 17.5.1
Breaking changes: feat(api)!: ... plus a BREAKING CHANGE: footer.

Open the PR against develop and fill in the template.

Before pushing:

bash
dart run build_runner build --delete-conflicting-outputs
dart format .
flutter analyze --fatal-infos
dart run custom_lint
flutter test
CI runs the same things plus an Android build. It needs to be green.

The rules
Rule	In short
Widgets hold no business logic	Visibility, animation, layout, simple navigation. Everything else goes in the ViewModel.
The UI never imports an SDK	No cloud_firestore, drift, or http outside data/datasources/. Screens see repositories and entities.
One direction	DataSource -> Repository -> ViewModel -> View. Events go back via ViewModel methods.
Typed errors	Repositories return Result<T>. SDK exceptions never reach the UI. Copy comes from AppFailure through l10n.
Immutable models	freezed. Don't mutate a list or object in place.
No hardcoded style	Colors, spacing, radii, durations, and fonts come from design tokens.
No literal user-facing strings	Everything through l10n (app_en.arb). No concatenated sentences.
No singletons	Injection goes through Riverpod so tests can fake it.
Declarative navigation	Nobody calls context.go(...) because auth changed. State changes; the guard moves the user.
If a rule is in the way, open an issue. Don't work around it in the PR.

Where things go
text
lib/
├── core/            # design system, router, database, notifications, errors, providers
└── features/<name>/
    ├── data/        # dtos, datasources, repository impls   <- SDKs live here
    ├── domain/      # entities, repository interfaces       <- knows about nobody
    └── presentation/# routes, view_models, screens, widgets
presentation knows domain. data implements domain. domain knows nobody.

Copy an existing feature if you're unsure, or ask in the issue first.

Tests
Write a unit test when a silent break would not be obvious to the user:

navigation guards and session state

date, time, and recurrence math

error mapping (FirebaseException → AppFailure)

DTO/entity transforms

multi-step operations that must not half-fail (sign-out, sync)

DAO queries and schema migrations

ViewModels with real branching

Skip widgets, tokens, one-line providers, and ViewModels that only forward a stream. A PR with no tests is fine when nothing critical changed. Say so in the description.

Tests are plain Dart: drive the notifier through a ProviderContainer with fake repositories. No tester, no pumpWidget.

Review
I aim to reply within 72 hours. A ping after that is welcome.

Small PRs merge faster than a 2000-line change across six features.

Screenshots or a recording for anything visible.

I squash-merge. The squashed title becomes the changelog entry, so make it a conventional commit.

License
By contributing, your work is licensed under the MIT License. There is no CLA.