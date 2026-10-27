# botmaker-plugin-parent

The parent pom a [BotMaker](https://github.com/BotMakerDev) Studio plugin inherits.

```xml
<parent>
    <groupId>com.github.BotMakerDev</groupId>
    <artifactId>botmaker-plugin-parent</artifactId>
    <version>v0.1.0</version>
    <relativePath/>
</parent>

<properties>
    <botmaker.plugin>com.example.greetings.plugin.ExamplePlugin</botmaker.plugin>
</properties>

<repositories>
    <repository>
        <id>jitpack.io</id>
        <url>https://jitpack.io</url>
    </repository>
</repositories>
```

The plugin declares the jitpack repository itself: Maven finds a parent through the child's repositories.

## What it gives a plugin

- **One version to move.** `botmaker-studio-api`, `botmaker-plugin-toolkit` and `javafx-controls` (`provided`)
  are pinned together in `dependencyManagement`, so the plugin's dependencies name no version. Setting
  `botmaker.studioapi.version` or `botmaker.plugintoolkit.version` in the plugin's own `<properties>` overrides
  one of them.
- **Java 25**, UTF-8, the compiler with `-parameters`, surefire.
- **A self-contained published pom.** flatten runs in every plugin: it writes the pins out, drops the
  `<parent>`, and keeps `<repositories>` and `<properties>` — `<botmaker.plugin>` is what makes the jar a
  plugin, and a host reads it off the pom Maven copies into the jar.

Released from the umbrella with the contract and the toolkit it pins; JitPack serves each tag as
`com.github.BotMakerDev:botmaker-plugin-parent:<tag>`.
