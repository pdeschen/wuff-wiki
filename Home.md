![Wuff logo](images/robo-dog_60x64.png)

Wuff is a gradle plugin for developing and assembling Eclipse applications and plugins **independently** of Eclipse-IDE. 

### Main features
Wuff does the following for you:
- downloads and "mavenizes" Eclipse bundles.
- generates runnable Equinox/RCP/IDE products for multiple platforms and locales.
- generates and merges OSGi manifests.
- generates and merges plugin.xml.
- generates and merges plugin_customization.ini.
- integrates splash.bmp into RCP/IDE app.
- integrates intro pages into RCP/IDE app.
- wraps non-OSGi dependencies into OSGi-bundles.

Every wuff feature is highly automated yet fully configurable.

### Prerequisites and usage

The following is required to start using Wuff:
- JDK version 7 or 8
- gradle version 1.11 or newer
- http-access to jcenter

Eclipse is not required - wuff will download and configure it automatically.

Wuff is available as maven artifact 'org.akhikhl.wuff:wuff-plugin:+' at jcenter and maven central.

The following chapters show how to use Wuff in "build.gradle".

### Equinox

- [Create first Equinox app](Create-first-Equinox-app)
- [Configure Equinox products](Configure-Equinox-products)
- [Prepare Equinox app for multi-project build](Prepare-Equinox-app-for-multiproject-build)
- [Create OSGi-bundle and use it in Equinox app](Create-OSGi-bundle-and-use-it-in-Equinox-app)

### Eclipe RCP

- [Create first RCP app](Create-first-RCP-app)
- [Configure RCP products](Configure-RCP-products)
- [Prepare RCP app for multiproject build](Prepare-RCP-app-for-multiproject-build)
- [Create Eclipse bundle and use it in RCP app](Create-Eclipse-bundle-and-use-it-in-RCP-app)
- [Add splash to RCP app](Add-splash-to-RCP-app)
- [Add intro page to RCP app](Add-intro-page-to-RCP-app)
- [Localize RCP app](Localize-RCP-app)

### Eclipse IDE

- [Create first IDE app](Create-first-IDE-app)
- [Configure IDE products](Configure-IDE-products)
- [Prepare IDE app for multiproject build](Prepare-IDE-app-for-multiproject-build)
- [Create IDE bundle and use it in IDE app](Create-IDE-bundle-and-use-it-in-IDE-app)
- [Add perspective and view to IDE app](Add-perspective-and-view-to-IDE-app)
- [Add splash to IDE app](Add-splash-to-IDE-app)
- [Add intro page to IDE app](Add-intro-page-to-IDE-app)
- [Localize IDE app](Localize-IDE-app)

### Programming manifests

- [Default manifest](Default-manifest)
- [Manifest attributes in build.gradle](Manifest-attributes-in-build.gradle)
- [Manifest attributes in MANIFEST.MF](Manifest-attributes-in-MANIFEST.MF)
- [Manifest expression injection](Manifest-expression-injection)

### Programming "plugin.xml"

- [Default "plugin.xml"](Default-plugin.xml)
- ["plugin.xml" for Eclipse bundle](plugin.xml-for-eclipse-bundle)
- ["plugin.xml" for Equinox app](Plugin.xml-for-eclipse-equinox-app)
- ["plugin.xml" for RCP app](Plugin.xml-for-eclipse-rcp-app)
- ["plugin.xml" for IDE app](Plugin.xml-for-eclipse-ide-app)
- ["plugin.xml" expression injection](plugin.xml-expression-injection)

### Dependency management

- [OSGi vs. non-OSGi dependencies](OSGi-vs.-non-OSGi-dependencies)
- [Wrapping non-OSGi libraries](Wrapping-non-OSGi-libraries)
- [PrivateLib configuration](PrivateLib-configuration)

[Examples](Examples)

[Programmer's reference](Programmers-reference)

[FAQ](Faq)