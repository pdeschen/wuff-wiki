We already learned what are [main features](Main-features) of Wuff. Now we consider what is required to start using Wuff:
- JDK version 7 or 8
- gradle version 1.11 or newer
- http-access to jcenter

Eclipse is not required. Wuff downloads and configures it automatically, from the official sources.

Wuff is a set of gradle plugins, that means - using Wuff is writing gradle scripts. Luckily, there's not much work to do. We create "build.gradle", add jcenter as maven repository, add instruction like `apply plugin: "eclipse-ide-app"` and that's it. All heavylifting - including OSGi dependencies, Equinox configuration etc.etc. - Wuff does for us automatically.

From here you can jump right to the examples: [first Equinox app](Create-first-Equinox-app), [first RCP app](Create-first-RCP-app), [first IDE app](Create-first-IDE-app) or systematically learn more about [gradle plugins](Gradle-plugins) provided by Wuff.