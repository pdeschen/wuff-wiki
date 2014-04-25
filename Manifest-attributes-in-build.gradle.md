We already inspected how [default manifest](Default-manifest) looks like. Now we will program manifest attributes in build.gradle.

1. Edit the file "tutorials/MyOsgiBundle/build.gradle", insert the code:

  ```groovy
  jar {
    manifest {
      instruction 'Bundle-SymbolicName', 'blabla'
      instruction 'Bundle-Name', 'hurray! hurray!'
      instruction 'Bundle-Version', '999'
      instruction 'Bundle-ManifestVersion', '22'
      instruction 'Bnd-LastModified', '9999999999999'                                    
      instruction 'Created-By', 'Dr. Who'
      instruction 'Tool', 'kekek'
      instruction 'Bundle-Classpath', 'somefolder', 'anotherfolder'
      instruction 'Require-Bundle', 'ch.qos.logback.classic'
      instruction 'My-Attribute', 'test'
    }
  }
  ```

  Here we configure "manifest" property of the Jar task. Note that manifest supports interface [OsgiManifest](http://www.gradle.org/docs/current/javadoc/org/gradle/api/plugins/osgi/OsgiManifest.html). This is because Wuff implicitly applies gradle 'osgi' plugin to the project.

2. Invoke on command line:

  ```
  gradle build
  ```

3. Open file "tutorials/MyOsgiPlugin/build/libs/MyOsgiPlugin-1.0.0.0.jar", open "META-INF/MANIFEST.MF", it should look like:

  ```
  Manifest-Version: 1.0
  Export-Package: 999
  Bundle-SymbolicName: MyOsgiPlugin
  Bundle-Name: MyOsgiPlugin
  Bundle-Version: 1.0.0.0
  Bundle-Classpath: .
  Require-Bundle: org.eclipse.osgi,ch.qos.logback.classic
  Bundle-ManifestVersion: 2
  Bnd-LastModified: 1398410836000
  My-Attribute: test
  Created-By: 1.8.0_05 (Oracle Corporation)
  Tool: Bnd-2.1.0.20130426-122213
  ```

  Note that Wuff ignores our values for attributes "Bundle-SymbolicName", "Bundle-Name", "Bundle-Version", "Bundle-ManifestVersion", "Bnd-LastModified", "Created-By", "Tool", "Bundle-Classpath". This is intentional: the generated values always overwrite the user-supplied values.

  There are three attributes that Wuff merges rather than overwrites: "Require-Bundle", "Import-Package" and "Export-Package". In the example above, our value "ch.qos.logback.classic" was added to generated value "org.eclipse.osgi".

