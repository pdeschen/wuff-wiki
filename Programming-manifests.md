We can program OSGi manifests for our bundles in two places:
- in file "META-INF/MANIFEST.MF" (it can reside in the project directory or in "src/main/resources")
- in "build.gradle", via jar/manifest structure.

We can also completely omit OSGi manifest. In such case Wuff generates *default manifest* for us. Wuff uses various project properties - version, name, dependencies, classpath etc. - as input for manifest generation. The default manifest does not pollute program sources: it is generated as a temporary file in buildDir and added to the resulting JAR file.

Even if we specified OSGi manifest either in "META-INF/MANIFEST.MF" or in "build.gradle" (or both), the default manifest is still generated and merged with our version in the following order:

    resulting manifest << build.gradle jar/manifest
    resulting manifest << default manifest
    resulting manifest << META-INF/MANIFEST.MF

Any attributes specified in "build.gradle" are overwritten by attributes in default manifest, which, in turn, are overwritten by attributes of user-provided "MANIFEST.MF".

There are four attributes that Wuff merges as lists rather than overwrites: "Require-Bundle", "Import-Package", "Export-Package" and "Bundle-ClassPath".

In this tutorial we will inspect default manifest and learn how to augment it.

- [Default manifest](Default-manifest)
- [Manifest attributes in build.gradle](Manifest-attributes-in-build.gradle)
- [Manifest attributes in MANIFEST.MF](Manifest-attributes-in-MANIFEST.MF)
- [Manifest expression injection](Manifest-expression-injection)
