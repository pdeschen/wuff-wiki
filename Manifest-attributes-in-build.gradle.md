We already inspected how [default manifest](Default-manifest) looks like. Now we will program manifest attributes in build.gradle.

1. Edit the file "tutorials/MyOsgiBundle/build.gradle", insert the code:

  ```groovy
  jar {
    manifest {
      instruction 'Require-Bundle', 'ch.qos.logback.classic'
    }
  }
  ```

  Here we configure "manifest" property of the Jar task. Note that manifest supports interface [OsgiManifest](http://www.gradle.org/docs/current/javadoc/org/gradle/api/plugins/osgi/OsgiManifest.html). This is because Wuff implicitly applies gradle 'osgi' plugin to the project.

2. Invoke on command line:

  ```
  gradle build
  ```

3. Open file "tutorials/MyOsgiPlugin/build/libs/MyOsgiPlugin-1.0.0.0.jar", open "META-INF/MANIFEST.MF", it should contain:

  ```
  Manifest-Version: 1.0
  Bundle-SymbolicName: MyOsgiPlugin
  Bundle-Version: 1.0.0.0
  Bundle-Name: MyOsgiPlugin
  Require-Bundle: org.eclipse.osgi,ch.qos.logback.classic
  Bundle-ManifestVersion: 2
  Bnd-LastModified: 1398405725000
  Created-By: 1.8.0_05 (Oracle Corporation)
  Tool: Bnd-2.1.0.20130426-122213
  Bundle-Classpath: .
  ```

  Note that Require-Bundle attribute now contains two entries: "ch.qos.logback.classic" and "org.eclipse.osgi". Wuff merges the 