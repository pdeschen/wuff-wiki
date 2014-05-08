On this page we will generate and inspect default OSGi manifest.

### Create "build.gradle"

Create folder "tutorials/MyOsgiManifest", create file "build.gradle" in it, insert code:

```groovy
buildscript {
  repositories {
    mavenLocal()
    jcenter()
  }

  dependencies {
    classpath 'org.akhikhl.wuff:wuff-plugin:+'
  }
}

apply plugin: 'java'
apply plugin: 'osgi-bundle'

repositories {
  mavenLocal()
  jcenter()
}
```

### Compile

Invoke on command line: `gradle build`.

### Inspect default manifest

Open file "tutorials/MyOsgiPlugin/build/libs/MyOsgiPlugin-1.0.0.0.jar", open "META-INF/MANIFEST.MF", it should contain something like this:

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

This is how the default manifest is generated:

- Bundle-SymbolicName and Bundle-Name are assigned to project name.
- Bundle-Version is assigned to project version. If project version is not specified in "build.gradle", the default value "1.0.0.0" is used for Bundle-Version.
- Require-Bundle is assigned to "org.eclipse.osgi" because of `apply plugin: 'osgi-bundle'` in "build.gradle".
- Bundle-Classpath is assigned to "root folder" in the context of JAR-file.
- All other fields are specific to BND-tool, which is invoked via chain Wuff -> gradle 'osgi' plugin -> BND-tool.

---

The example code for this page: [examples/Manifest-1](../tree/master/examples/Manifest-1).

Next page: [Manifest attributes in build.gradle](Manifest-attributes-in-build.gradle).