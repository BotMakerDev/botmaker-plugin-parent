# CLAUDE.md

Guidance for working in **botmaker-plugin-parent**, the parent pom a BotMaker plugin names.

Read the umbrella `../CLAUDE.md` first, and `../docs/refactor/24-plugin-platform.md` §10 for what makes a jar a
plugin.

## What it is

One pom, packaging `pom`, no sources. What every plugin's pom would otherwise repeat: the contract, the toolkit
and JavaFX pinned together (`dependencyManagement`), Java 25, the compiler (3.11.0, `-parameters`), surefire, and
flatten 1.4.1 `oss` keeping `repositories` and `properties`.

## Rules

- **Nothing that identifies one plugin**: no `botmaker.plugin`, no `<name>`. `<properties>` are inherited.
- **No `<repositories>`**: a child finds this parent through its own, so it declares jitpack.io itself.
- **flatten is in `<plugins>`, not only `<pluginManagement>`**, so every child runs it; this pom is not
  replaced by its flattened copy (`updatePomFile` is false for packaging `pom`).
- **Pins move only by the release library** (`botmaker.studioapi.version`, `botmaker.plugintoolkit.version`),
  like every module's. A child pins this module by its `<parent><version>`, which the release library moves with
  `versions:update-parent`.
- Every pin is held to JitPack's Maven 3.9.9 ceiling (umbrella § JitPack).

## Building

```bash
mvn install     # installs this pom at its main -SNAPSHOT
```

Published through JitPack. Released from the umbrella (`--plugin-parent`); the contract and the toolkit force a
release here, and a release here forces the archetype.
