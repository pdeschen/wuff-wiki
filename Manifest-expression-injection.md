We already programmed [manifest attributes in MANIFEST.MF](Manifest-attributes-in-MANIFEST.MF). Now we will learn how to do manifest expression injection.

### Manifest expression injection in "build.gradle"

The easiest way to do manifest expression injection is to use gradle/groovy capabilities. Edit file "tutorials/MyOsgiPlugin/build.gradle", insert code to jar/manifest:

```groovy
instruction 'Project-Info', "${project.name} compiled on ${new Date()}"
```

Invoke on command line: `gradle build`.

Open file "tutorials/MyOsgiPlugin/build/libs/MyOsgiPlugin-1.0.0.0.jar", open "META-INF/MANIFEST.MF", it should contain:

```
Project-Info: MyOsgiPlugin compiled on Fri Apr 25 12:46:22 CEST 2014
```

### Manifest expression injection in MANIFEST.MF

We can also program expression injection in MANIFEST.MF. Edit the file "tutorials/MyOsgiPlugin/src/main/resources/META-INF/MANIFEST.MF", insert code:

```
Project-Description: ${project.description}
```

Edit file "tutorials/MyOsgiPlugin/build.gradle", insert code:

```groovy
description = 'this is example project'

wuff {
  filterManifest = true
}
```

Invoke on command line: `gradle build`

Open file "tutorials/MyOsgiPlugin/build/libs/MyOsgiPlugin-1.0.0.0.jar", open "META-INF/MANIFEST.MF", it should contain:

```
Project-Description: this is example project
```

Note that expressions in MANIFEST.MF are **not** expanded by default. We must set `wuff.filterManifest=true` to enable this feature.

---

The example code for this page: [examples/Manifest-4](../tree/master/examples/Manifest-4).

We are done with programming manifests. Now we can go back to [wiki home page](Home) and learn something else.