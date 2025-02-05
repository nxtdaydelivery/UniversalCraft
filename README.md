# UniversalCraft

A full Java interop library that wraps Minecraft classes which allows you to write code for multiple versions at the same time. Built using ReplayMod's [Preprocessor](https://github.com/ReplayMod/preprocessor).

## Dependency

It's recommended that you include [Essential](link eventually) instead of adding it yourself.

In your repository block, add:

Groovy
```groovy
maven {
    url = "https://repo.essential.gg/repository/maven-public"
}
```
Kotlin
```kotlin
maven(url = "https://repo.essential.gg/repository/maven-public")
```

To use the latest builds, use the following dependency format, use the build reference to find the correct replacements:

<details><summary>Forge</summary>

```kotlin
implementation("gg.essential:universalcraft-$mcVersion-$mcPlatform:$buildNumber")
```
</details>
<details><summary>Fabric</summary>

Groovy
```groovy
modImplementation(include("gg.essential:universalcraft-$mcVersion-$mcPlatform:$buildNumber"))
```
Kotlin
```kotlin
modImplementation(include("gg.essential:universalcraft-$mcVersion-$mcPlatform:$buildNumber")!!)
```
</details>

### Build Reference
<details><summary>Build Reference</summary>
    <table>
      <tbody>
        <tr>
          <th>mcVersion</th>
          <th>mcPlatform</th>
          <th>buildNumber</th>
        </tr>
        <tr>
          <td>1.18.1</td>
          <td>fabric</td>
          <td>
            <img alt="1.18.1-fabric" src="https://badges.modcore.net/badge/dynamic/xml?color=A97BFF&label=%20&query=%2Fmetadata%2Fversioning%2Flatest&url=https://repo.essential.gg/repository/maven-releases/gg/essential/universalcraft-1.18.1-fabric/maven-metadata.xml">
          </td>
        </tr>
        <tr>
          <td>1.18.1</td>
          <td>forge</td>
          <td>
            <img alt="1.18.1-forge" src="https://badges.modcore.net/badge/dynamic/xml?color=A97BFF&label=%20&query=%2Fmetadata%2Fversioning%2Flatest&url=https://repo.essential.gg/repository/maven-releases/gg/essential/universalcraft-1.18.1-forge/maven-metadata.xml">
          </td>
        </tr>
        <tr>
          <td>1.17.1</td>
          <td>fabric</td>
          <td>
            <img alt="1.17.1-fabric" src="https://badges.modcore.net/badge/dynamic/xml?color=A97BFF&label=%20&query=%2Fmetadata%2Fversioning%2Flatest&url=https://repo.essential.gg/repository/maven-releases/gg/essential/universalcraft-1.17.1-fabric/maven-metadata.xml">
          </td>
        </tr>
        <tr>
          <td>1.17.1</td>
          <td>forge</td>
          <td>
            <img alt="1.17.1-forge" src="https://badges.modcore.net/badge/dynamic/xml?color=A97BFF&label=%20&query=%2Fmetadata%2Fversioning%2Flatest&url=https://repo.essential.gg/repository/maven-releases/gg/essential/universalcraft-1.17.1-forge/maven-metadata.xml">
          </td>
        </tr>
        <tr>
          <td>1.16.2</td>
          <td>forge</td>
          <td>
            <img alt="1.16.2-forge" src="https://badges.modcore.net/badge/dynamic/xml?color=A97BFF&label=%20&query=%2Fmetadata%2Fversioning%2Flatest&url=https://repo.essential.gg/repository/maven-releases/gg/essential/universalcraft-1.16.2-forge/maven-metadata.xml">
          </td>
        </tr>
        <tr>
          <td>1.12.2</td>
          <td>forge</td>
          <td>
            <img alt="1.12.2-forge" src="https://badges.modcore.net/badge/dynamic/xml?color=A97BFF&label=%20&query=%2Fmetadata%2Fversioning%2Flatest&url=https://repo.essential.gg/repository/maven-releases/gg/essential/universalcraft-1.12.2-forge/maven-metadata.xml">
          </td>
        </tr>
        <tr>
          <td>1.8.9</td>
          <td>forge</td>
          <td>
            <img alt="1.8.9-forge" src="https://badges.modcore.net/badge/dynamic/xml?color=A97BFF&label=%20&query=%2Fmetadata%2Fversioning%2Flatest&url=https://repo.essential.gg/repository/maven-releases/gg/essential/universalcraft-1.8.9-forge/maven-metadata.xml">
          </td>
        </tr>
      </tbody>
    </table>

</details>

<h2><span style="font-size:3em; color:red;">IMPORTANT!</span></h2>

If you are using forge, you must also relocate UC to avoid potential crashes with other mods. To do this, you will need to use the Shadow Gradle plugin.

<details><summary>Groovy Version</summary>

You can do this by either putting it in your plugins block:
```groovy
plugins {
    id "com.github.johnrengelman.shadow" version "$version"
}
```
or by including it in your buildscript's classpath and applying it:
```groovy
buildscript {
    repositories {
        gradlePluginPortal()
    }
    dependencies {
        classpath "gradle.plugin.com.github.jengelman.gradle.plugins:shadow:$version"
    }
}

apply plugin: "com.github.johnrengelman.shadow"
```
You'll then want to relocate UC to your own package to avoid breaking other mods
```groovy
shadowJar {
    archiveClassifier.set(null)
    relocate("gg.essential.universal", "your.package.universal")
}
tasks.named("reobfJar").configure { dependsOn(tasks.named("shadowJar")) }
```

</details>

<details><summary>Kotlin Script Version</summary>

You can do this by either putting it in your plugins block:
```kotlin
plugins {
    id("com.github.johnrengelman.shadow") version "$version"
}
```
or by including it in your buildscript's classpath and applying it:
```kotlin
buildscript {
    repositories {
        gradlePluginPortal()
    }
    dependencies {
        classpath("gradle.plugin.com.github.jengelman.gradle.plugins:shadow:$version")
    }
}

apply(plugin = "com.github.johnrengelman.shadow")
```
You'll then want to relocate UC to your own package to avoid breaking other mods
```kotlin
tasks.shadowJar {
    archiveClassifier.set(null)
    relocate("gg.essential.universal", "your.package.universal")
}
tasks.reobfJar { dependsOn(tasks.shadowJar) }
```

</details>