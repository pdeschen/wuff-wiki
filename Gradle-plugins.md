Wuff provides the following gradle plugins:

- osgi-bundle

  Configures current project as Eclipse plugin, so that gradle build:
  - injects trivial OSGi dependencies
  - generates and merges OSGi manifest

  Usage: `apply plugin: 'osgi-bundle'`.

- eclipse-bundle

  Configures current project as Eclipse plugin, so that gradle build:
  - injects trivial Eclipse dependencies
  - generates and merges OSGi manifest
  - generates and merges plugin.xml

  Usage: `apply plugin: 'eclipse-bundle'`.

- eclipse-equinox-app

  Configures current project as Equinox app, so that gradle build:
  - injects trivial Eclipse dependencies
  - generates and merges OSGi manifest
  - generates and merges plugin.xml
  - generates and merges plugin_customization.ini
  - wraps non-OSGi dependencies into OSGi-bundles
  - generates runnable Eclipse Equinox products for multiple platforms and locales

  Usage: `apply plugin: 'eclipse-equinox-app'`.

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

- eclipse-ide-bundle

  Very similar to eclipse-bundle, only adds "org.eclipse.ui.ide" as dependency

  Usage: `apply plugin: 'eclipse-ide-bundle'`.

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
