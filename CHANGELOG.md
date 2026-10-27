# Changelog

All notable changes to `botmaker-plugin-parent`.

The format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/), and this module uses
[semantic versioning](https://semver.org/). The release refuses to cut a version with no section here.

## [Unreleased]

### Added

- **The parent pom a BotMaker plugin names** (2026-10-27). `dependencyManagement` pins `botmaker-studio-api`,
  `botmaker-plugin-toolkit` and `javafx-controls` (`provided`) together; Java 25 and UTF-8; the compiler at
  3.11.0 with `-parameters`, surefire 3.2.5, and flatten 1.4.1 in `oss` mode keeping `repositories` and
  `properties`, so a plugin's published pom keeps `<botmaker.plugin>` and names no parent.
