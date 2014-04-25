We already programmed [manifest attributes in build.gradle](Manifest-attributes-in-build.gradle). Now we will program manifest attributes in MANIFEST.MF.

1. Create folder "tutorials/MyOsgiPlugin/src/main/resources/META-INF", create file "MANIFEST.MF" in it, insert code:

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

2. Invoke on command line:

  ```
  gradle build
  ```

3. Open file "tutorials/MyOsgiPlugin/build/libs/MyOsgiPlugin-1.0.0.0.jar", open "META-INF/MANIFEST.MF", it should look like:

  ```
  Manifest-Version: 1.0
  Bundle-SymbolicName: MyOsgiPlugin
  Bundle-Name: MyOsgiPlugin
  Bundle-Version: 1.0.0.0
  Bundle-Classpath: .
  Require-Bundle: org.eclipse.jface.text,org.eclipse.osgi,ch.qos.logback
    .classic
  Bundle-ManifestVersion: 2
  Bnd-LastModified: 1398419098000
  My-Attribute: test2
  Created-By: 1.8.0_05 (Oracle Corporation)
  Tool: Bnd-2.1.0.20130426-122213
  ```

  Note that Wuff ignores our values for attributes "Bundle-SymbolicName", "Bundle-Name", "Bundle-Version", "Bundle-ManifestVersion", "Bnd-LastModified", "Created-By", "Tool", "Bundle-Classpath". This is intentional: Wuff overwrites the user-supplied attributes with the generated attributes having the same name.

  There are three attributes that Wuff merges rather than overwrites: "Require-Bundle", "Import-Package" and "Export-Package". In the example above, "Require-Bundle" contains three values: "org.eclipse.osgi" comes from generated manifest, "ch.qos.logback.classic" comes from "build.gradle" and "org.eclipse.jface.text" comes from MANIFEST.MF.

  Note that "My-Attribute" was specified in two places: in "build.gradle" and "MANIFEST.MF". The values of "MANIFEST.MF" overwrite the values of "build.gradle".