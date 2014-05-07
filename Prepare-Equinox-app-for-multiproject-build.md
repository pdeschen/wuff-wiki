We already [configured Equinox products](Configure-Equinox-products). Now we prepare Equinox app for multiproject build.

### Create root "build.gradle"

Create "build.gradle" in "tutorials" folder (parent of "MyRcpApp" folder) 

Move "buildscript" and "repositories" from "tutorials/MyRcpApp/build.gradle" to "tutorials/build.gradle", so that two scripts look like this:

"tutorials/build.gradle":
```groovy
buildscript {
  repositories {
    mavenLocal()
    jcenter()
  }
  
  dependencies {
    classpath 'org.akhikhl.wuff:wuff-plugin:0.0.3'
  }
}

subprojects {
  repositories {
    mavenLocal()
    jcenter()
  }
}
```

"tutorials/MyRcpApp/build.gradle":
```groovy
apply plugin: 'java'
apply plugin: 'eclipse-rcp-app'
  
products {
  product platform: 'linux', arch: 'x86_32'
  product platform: 'linux', arch: 'x86_64'
  product platform: 'windows', arch: 'x86_32'
  product platform: 'windows', arch: 'x86_64'
  archiveProducts = true
}
```

### Create "settings.gradle"

Create "settings.gradle" in "tutorials" folder (parent of "MyRcpApp" folder), insert code:

```groovy
include 'MyRcpApp'
```

### Compile

Invoke on command line in "tutorials" folder: `gradle build`

Check: build task generates products in "tutorials/MyEquinoxApp/build/output" folder.

---

The example code for this page: [examples/EquinoxApp-3](../tree/master/examples/EquinoxApp-3).

Next page: [Create OSGi-bundle and use it in Equinox app](Create-OSGi-bundle-and-use-it-in-Equinox-app).