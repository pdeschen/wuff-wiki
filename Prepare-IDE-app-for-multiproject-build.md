We already [configured IDE products](Configure-IDE-products). Now we prepare IDE app for multiproject build.

### Create root "build.gradle"

Create "build.gradle" in "tutorials" folder (parent of "MyIdeApp" folder).

Move "buildscript" and "repositories" from "tutorials/MyIdeApp/build.gradle" to "tutorials/build.gradle", so that two scripts look like this:

"tutorials/build.gradle":
```groovy
buildscript {
  repositories {
    mavenLocal()
    jcenter()
  }
  
  dependencies {
    classpath 'org.akhikhl.wuff:wuff-plugin:0.0.1'
  }
}

subprojects {
  repositories {
    mavenLocal()
    jcenter()
  }
}
```

"tutorials/MyIdeApp/build.gradle":
```groovy
apply plugin: 'java'
apply plugin: 'eclipse-ide-app'
  
products {
  product platform: 'linux', arch: 'x86_32'
  product platform: 'linux', arch: 'x86_64'
  product platform: 'windows', arch: 'x86_32'
  product platform: 'windows', arch: 'x86_64'
  archiveProducts = true
}
```

### Create "settings.gradle"

Create "settings.gradle" in "tutorials" folder (parent of "MyIdeApp" folder), insert code:

```groovy
include 'MyIdeApp'
```

### Compile

Invoke on command line in "tutorials" folder: `gradle build`.

Check: build task must generate products in "tutorials/MyIdeApp/build/output" folder.

---

The example code for this page: [examples/IdeApp-3](../tree/master/examples/IdeApp-3).

Next page: [Create IDE bundle and use it in IDE app](Create-IDE-bundle-and-use-it-in-IDE-app).