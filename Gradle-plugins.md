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
  - generates runnable Equinox products for multiple platforms and locales.

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
  - generates runnable Equinox products for multiple platforms and locales.

  Usage: `apply plugin: 'eclipse-rcp-app'`.
