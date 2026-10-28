# CLAUDE.md

Guidance for working in **botmaker-plugin-parent**, the parent pom a BotMaker plugin names.

Read the umbrella `../CLAUDE.md` first, and `../docs/refactor/24-plugin-platform.md` §10 for what makes a jar a
plugin.

## What it is

One pom, packaging `pom`, no sources. What every plugin's pom would otherwise repeat: the contract, the toolkit
and JavaFX pinned together (`dependencyManagement`), Java 25, the compiler (3.11.0, `-parameters`), surefire, and
flatten 1.4.1 `oss` keeping `repositories` and `properties`, and antrun 3.1.0 copying the plugin's
`CHANGELOG.md` and `icon.png` into the jar as `META-INF/botmaker/changelog.md` and `icon.png` (Studio's
`PluginJarFiles`), each skipped when missing, and `maven-source-plugin` 3.3.0 attaching a `-sources.jar`, where
Studio reads a plugin's `@Migrate` rules (2026-10-28).

## Rules

- **Nothing that identifies one plugin**: no `botmaker.plugin`, no `<name>`. `<properties>` are inherited.
- **No `<repositories>`**: a child finds this parent through its own, so it declares jitpack.io itself.
- **flatten is in `<plugins>`, not only `<pluginManagement>`**, so every child runs it; this pom is not
  replaced by its flattened copy (`updatePomFile` is false for packaging `pom`).
- **Pins move only by the release library** (`botmaker.studioapi.version`, `botmaker.plugintoolkit.version`),
  like every module's. A child pins this module by its `<parent><version>`, which the release library moves as a
  literal (`PomVersions.parentVersion`): any Maven mojo would first resolve the `-SNAPSHOT` parent it replaces.
- Every pin is held to JitPack's Maven 3.9.9 ceiling (umbrella § JitPack).

## Building

```bash
mvn install     # installs this pom at its main -SNAPSHOT
```

Published through JitPack. Released from the umbrella (`--plugin-parent`); the contract and the toolkit force a
release here, and a release here forces the archetype.
