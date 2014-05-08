We already inspected how [default manifest](Default-manifest) looks like. Now we will program manifest attributes in build.gradle.

### Add manifest attributes to "build.gradle"

Edit the file "tutorials/MyOsgiBundle/build.gradle", insert the code:

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
    instruction 'Bundle-ClassPath', 'somefolder', 'anotherfolder'
    instruction 'Require-Bundle', 'ch.qos.logback.classic'
    instruction 'My-Attribute', 'test'
  }
}
```

Here we configure "manifest" property of the Jar task. Note that manifest supports interface [OsgiManifest](http://www.gradle.org/docs/current/javadoc/org/gradle/api/plugins/osgi/OsgiManifest.html). This is because Wuff implicitly applies gradle 'osgi' plugin to the project.

### Compile

Invoke on command line: `gradle build`.

### Inspect resulting manifest

Open file "tutorials/MyOsgiPlugin/build/libs/MyOsgiPlugin-1.0.0.0.jar", open "META-INF/MANIFEST.MF", it should look like:

```
Manifest-Version: 1.0
Bundle-SymbolicName: MyOsgiPlugin
Bundle-Name: MyOsgiPlugin
Bundle-Version: 1.0.0.0
Bundle-ClassPath: somefolder,.,anotherfolder
Require-Bundle: org.eclipse.osgi,ch.qos.logback.classic
Bundle-ManifestVersion: 2
Bnd-LastModified: 1399560688000
My-Attribute: test
Created-By: 1.8.0_05 (Oracle Corporation)
Tool: Bnd-2.1.0.20130426-122213
```

As we see, Wuff overwritten our values for attributes "Bundle-SymbolicName", "Bundle-Name", "Bundle-Version", "Bundle-ManifestVersion", "Bnd-LastModified", "Created-By", "Tool". This is caused by the sequence of manifest merge: resulting-manifest << build.gradle << default-manifest.

There are four attributes that Wuff merges rather than overwrites: "Require-Bundle", "Import-Package", "Export-Package" and "Bundle-ClassPath". In the example above, "Require-Bundle" contains two values: "ch.qos.logback.classic" comes from "build.gradle" and "org.eclipse.osgi" comes from default manifest. Also we see, that "Bundle-ClassPath" contains three values: "somefolder" and "anotherfolder" come from "build.gradle", "." comes from default manifest.

---

The example code for this page: [examples/Manifest-2](../tree/master/examples/Manifest-2).

Next page: [Manifest attributes in MANIFEST.MF](Manifest-attributes-in-MANIFEST.MF).
