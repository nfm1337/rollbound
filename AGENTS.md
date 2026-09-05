# Repository Guidelines

## Project Structure & Module Organization

Rollbound is a Kotlin/libGDX project split into three Gradle modules:

- `core/`: platform-independent game logic under `src/main/kotlin/io/github/nfm1337`.
- `lwjgl3/`: desktop launcher, packaging configuration, icons, and native-image support.
- `android/`: Android launcher, manifest, resources, and ProGuard rules.
- `assets/`: shared runtime textures, fonts, skins, and other game data. Both launchers consume this directory.

Keep gameplay code in `core`; platform modules should contain only startup code and platform-specific integrations. Generated output belongs in module `build/` directories and must not be committed.

## Build, Test, and Development Commands

Use the checked-in Gradle wrapper. On Windows, run:

- `.\gradlew.bat lwjgl3:run` — launch the desktop build using `assets/` as its working directory.
- `.\gradlew.bat build` — compile and package all configured modules.
- `.\gradlew.bat test` — run all unit tests.
- `.\gradlew.bat lwjgl3:jar` — create the runnable desktop JAR in `lwjgl3/build/libs/`.
- `.\gradlew.bat android:assembleDebug` — build a debug APK; this requires a configured Android SDK.
- `.\gradlew.bat android:lint` — run Android validation.

On macOS or Linux, replace `.\gradlew.bat` with `./gradlew`.

## Coding Style & Naming Conventions

Follow `.editorconfig`: UTF-8, LF endings, final newlines, four-space indentation for Kotlin/Java, and two spaces for Gradle files. Use Kotlin conventions: `PascalCase` for classes and screens, `camelCase` for functions and properties, and lowercase package paths rooted at `io.github.nfm1337`. Prefer small, lifecycle-aware libGDX components and dispose textures, batches, and other native resources explicitly.

## Testing Guidelines

No tests or coverage threshold are currently defined. Add shared tests under `core/src/test/kotlin`, mirroring production packages, and name classes `*Test` (for example, `MovementSystemTest`). Add the chosen test dependency to `core/build.gradle`. Keep logic testable without launching a graphics context; reserve integration checks for launcher-specific behavior. Run `.\gradlew.bat test` before submitting changes.

## Commit & Pull Request Guidelines

Use Conventional Commits in the form `<type>(<optional scope>): <description>`. Keep descriptions short and imperative, and keep each commit focused. Common types include `feat`, `fix`, `docs`, `style`, `refactor`, `test`, `chore`, `perf`, and `ci`; for example, `feat(core): add player movement` or `chore(quality): configure Kotlin linting`. Pull requests should explain behavior changes, identify affected platforms, link relevant issues, and list verification commands. Include screenshots or a short capture for visible UI/gameplay changes, and call out new assets or configuration requirements.

## Configuration & Assets

Do not commit machine-specific `local.properties`, SDK paths, credentials, or generated binaries. Use stable, lowercase asset names, update references when moving files, and verify asset loading on both desktop and Android.
