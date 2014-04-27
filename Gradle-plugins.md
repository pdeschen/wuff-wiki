Wuff provides the following gradle plugins:

- osgi-bundle

  Configures current project as Eclipse plugin, so that gradle build:
  - injects trivial OSGi dependencies
  - generates and merges OSGi manifest

  Usage: `apply plugin: 'osgi-bundle'`.

  There is concrete example of using osgi-bundle plugin on page [Create OSGi bundle and use it in Equinox app](Create-OSGi-bundle-and-use-it-in-Equinox-app).

- eclipse-bundle

  Configures current project as Eclipse plugin, so that gradle build:
  - injects trivial Eclipse dependencies
  - generates and merges OSGi manifest
  - generates and merges plugin.xml

  Usage: `apply plugin: 'eclipse-bundle'`.

  There is concrete example of using eclipse-bundle plugin on page [Create Eclipse bundle and use it in RCP app](Create-Eclipse-bundle-and-use-it-in-RCP-app).

- eclipse-equinox-app

  Configures current project as Equinox app, so that gradle build:
  - injects trivial Eclipse dependencies
  - generates and merges OSGi manifest
  - generates and merges plugin.xml
  - generates and merges plugin_customization.ini
  - wraps non-OSGi dependencies into OSGi-bundles
  - generates runnable Eclipse Equinox products for multiple platforms and locales

  Usage: `apply plugin: 'eclipse-equinox-app'`.

  There is concrete example of using eclipse-equinox-app plugin on page [
Create first Equinox app](Create-first-Equinox-app).

- eclipse-rcp-app

  Configures current project as Eclipse RCP app, so that gradle build:
  - injects trivial Eclipse dependencies
  - generates and merges OSGi manifest
  - generates and merges plugin.xml
  - generates and merges plugin_customization.ini
  - integrates splash.bmp
  - integrates intro pages
  - wraps non-OSGi dependencies into OSGi-bundles
  - generates runnable Eclipse RCP products for multiple platforms and locales

  Usage: `apply plugin: 'eclipse-rcp-app'`.

  There is concrete example of using eclipse-rcp-app plugin on page [
Create first RCP app](Create-first-RCP-app).

- eclipse-ide-app

  Configures current project as Eclipse IDE app, so that gradle build:
  - injects trivial Eclipse dependencies
  - generates and merges OSGi manifest
  - generates and merges plugin.xml
  - generates and merges plugin_customization.ini
  - integrates splash.bmp
  - integrates intro pages
  - wraps non-OSGi dependencies into OSGi-bundles
  - generates runnable Eclipse IDE products for multiple platforms and locales

  Usage: `apply plugin: 'eclipse-ide-app'`.

  There is concrete example of using eclipse-ide-app plugin on page [
Create first IDE app](Create-first-IDE-app).

- eclipse-ide-bundle

  Very similar to eclipse-bundle, only adds "org.eclipse.ui.ide" as dependency

  Usage: `apply plugin: 'eclipse-ide-bundle'`.

  There is concrete example of using eclipse-ide-bundle plugin on page [Create IDE bundle and use it in IDE app](Create-IDE-bundle-and-use-it-in-IDE-app).

- eclipse-config

  Does not configure project as bundle or application. Instead, it creates gradle project extension "wuff". Can be used for hierarchical Wuff configuration in multiproject setup.

  Usage: `apply plugin: 'eclipse-config'`.

- swt-lib

  Configures current project as non-OSGi SWT/JFace library, so that gradle build:
  - injects SWT and JFace dependencies

  Usage: `apply plugin: 'swt-lib'`.

- swt-app

  Configures current project as non-OSGi SWT/JFace app, so that gradle build:
  - injects SWT and JFace dependencies
  - generates runnable non-OSGi SWT/JFace products for multiple platforms and locales

  Usage: `apply plugin: 'swt-app'`.
