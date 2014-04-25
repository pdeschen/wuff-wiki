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