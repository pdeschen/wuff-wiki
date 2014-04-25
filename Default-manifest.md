Wuff generates default OSGi manifest for all applied Wuff plugins. It uses various project properties - version, name, dependencies, classpath etc. - as input for manifest generation. The default manifest does not pollute program sources: it is generated as a temporary file in buildDir.

If no additional configuration specified, the default manifest is used as the resulting "MANIFEST.MF" in the JAR-file.

If we program jar/manifest properties in "build.gradle", they are merged with the default manifest to produce the resulting "MANIFEST.MF" in the JAR-file.

If we provide our own MANIFEST.MF (either in "src/main/resources/META-INF" or in "META-INF"), it is merged with the default manifest to produce the resulting "MANIFEST.MF" in the JAR-file.

OSGI manifest merge is performed in the following order:

- resulting manifest << build.gradle jar/manifest
- resulting manifest << user-provided MANIFEST.MF
- resulting manifest << default manifest

Any attributes specified in "build.gradle" are overwritten by attributes in user-provided "MANIFEST.MF", which, in turn, are overwritten by attributes of default manifest.

Lets inspect how default manifest looks like.

1. Create folder "tutorials/MyOsgiManifest", create file "build.gradle" in it, insert code:

  ```groovy
  buildscript {
    repositories {
      mavenLocal()
      jcenter()
    }

    dependencies {
      classpath 'org.akhikhl.wuff:wuff-plugin:0.0.1'
    }
  }

  apply plugin: 'java'
  apply plugin: 'osgi-bundle'

  repositories {
    mavenLocal()
    jcenter()
  }
  ```

2. Invoke on command line:

  ```shell
  gradle build
  ```

3. Open file "tutorials/MyOsgiPlugin/build/libs/MyOsgiPlugin-1.0.0.0.jar", open "META-INF/MANIFEST.MF", it should contain something like this:

  ```
  Manifest-Version: 1.0
  Bundle-SymbolicName: MyOsgiPlugin
  Bundle-Version: 1.0.0.0
  Bundle-Name: MyOsgiPlugin
  Require-Bundle: org.eclipse.osgi
  Bundle-ManifestVersion: 2
  Bnd-LastModified: 1398375756000
  Created-By: 1.8.0_05 (Oracle Corporation)
  Tool: Bnd-2.1.0.20130426-122213
  Bundle-Classpath: .
  ```
  
  This is how default manifest is generated:

  - Bundle-SymbolicName and Bundle-Name are assigned to project name.
  - Bundle-Version is assigned to project version. If project version is not specified in "build.gradle", the default value "1.0.0.0" is used for Bundle-Version.
  - Require-Bundle is assigned to "org.eclipse.osgi" because of `apply plugin: 'osgi-bundle'` in "build.gradle".
  - Bundle-Classpath is assigned to "root folder" in the context of JAR-file.
  - All other fields are specific to BND-tool, which is invoked via chain Wuff -> gradle 'osgi' plugin -> BND-tool.

[1]: In Wuff context OSGi-bundle is a gradle project with one of the plugins applied: "eclipse-bundle", "eclipse-equinox-app", "eclipse-ide-app", "eclipse-ide-bundle", "eclipse-rcp-app", "osgi-bundle".

The example code for this page: [tutorialExamples/Manifest-1](../tree/master/tutorialExamples/Manifest-1).

Next page: [Manifest attributes in build.gradle](Manifest-attributes-in-build.gradle).