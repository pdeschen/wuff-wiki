We already programmed [manifest attributes in build.gradle](Manifest-attributes-in-build.gradle). Now we will program manifest attributes in MANIFEST.MF.

### Add manifest attributes to MANIFEST.MF

Create folder "tutorials/MyOsgiPlugin/src/main/resources/META-INF", create file "MANIFEST.MF" in it, insert code:

```
Bundle-SymbolicName: abcabc
Bundle-Name: someBundleName
Bundle-Version: 1212
Bundle-Classpath: aaaa,bbbb
Require-Bundle: org.eclipse.jface.text
Bundle-ManifestVersion: 2323
Bnd-LastModified: 8888888888888
Created-By: Batman
Tool: lololo
My-Attribute: test2
```

### Compile

Invoke on command line: `gradle build`.

### Inspect resulting manifest

Open file "tutorials/MyOsgiPlugin/build/libs/MyOsgiPlugin-1212.jar", open "META-INF/MANIFEST.MF", it should look like:

```
Manifest-Version: 1.0
Bundle-SymbolicName: abcabc
Bundle-Name: someBundleName
Bundle-Version: 1212
Bundle-ClassPath: anotherfolder,aaaa,somefolder,.,bbbb
Require-Bundle: org.eclipse.jface.text,org.eclipse.osgi,ch.qos.logback
 .classic
Bundle-ManifestVersion: 2323
Bnd-LastModified: 8888888888888
My-Attribute: test2
Created-By: Batman
Tool: lololo
```

We see that values for attributes "Bundle-SymbolicName", "Bundle-Name", "Bundle-Version", "Bundle-ManifestVersion", "Bnd-LastModified", "Created-By", "Tool" were overwritten with values from our MANIFEST.MF. This is caused by the sequence of manifest merge: resulting-manifest << build.gradle << default-manifest << MANIFEST.MF.

The attribute "Bundle-ClassPath" was merged from three places. "somefolder" and "anotherfolder" come from "build.gradle", "." comes from default manifest, "aaaa" and "bbbb" come from "MANIFEST.MF".

Note that "My-Attribute" was specified in two places: in "build.gradle" and "MANIFEST.MF". The value in "MANIFEST.MF" overwrites the value in "build.gradle".

---

The example code for this page: [examples/Manifest-3](../tree/master/examples/Manifest-3).

Next page: [Manifest expression injection](Manifest-expression-injection).