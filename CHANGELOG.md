# Changelog

All notable changes to `botmaker-plugin-parent`.

The format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and this module uses
[semantic versioning](https://semver.org/). The release refuses to cut a version with no section here.

## [0.1.0] — 2026-10-28

### Added

- **The parent pom a BotMaker plugin names** (2026-10-27). `dependencyManagement` pins `botmaker-studio-api`,
  `botmaker-plugin-toolkit` and `javafx-controls` (`provided`) together; Java 25 and UTF-8; the compiler at
  3.11.0 with `-parameters`, surefire 3.2.5, and flatten 1.4.1 in `oss` mode keeping `repositories` and
  `properties`, so a plugin's published pom keeps `<botmaker.plugin>` and names no parent.
- **A plugin's changelog and icon in its jar** (2026-10-28): antrun copies `CHANGELOG.md` to
  `META-INF/botmaker/changelog.md` (Studio's upgrade dialog shows the sections a bot crosses) and `icon.png` to
  `META-INF/botmaker/icon.png` (shown beside the plugin's name). Either may be missing.
- **A `-sources.jar` beside every plugin jar** (2026-10-28): `maven-source-plugin` 3.3.0 (`jar-no-fork`), so
  Studio can read the `@Migrate` rules a plugin ships beside a `@Deprecated(forRemoval = true)` element.
