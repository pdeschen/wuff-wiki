We already [configured SWT products](Configure-SWT-products). Now we prepare SWT app for multiproject build.

### Create root "build.gradle"

Create "build.gradle" in "tutorials" folder (parent of "MySwtApp" folder).

Move "buildscript" and "repositories" from "tutorials/MySwtApp/build.gradle" to "tutorials/build.gradle", so that two scripts look like this:

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

"tutorials/MySwtApp/build.gradle":
```groovy
apply plugin: 'java'
apply plugin: 'swt-app'
  
products {
  product platform: 'linux', arch: 'x86_32'
  product platform: 'linux', arch: 'x86_64'
  product platform: 'windows', arch: 'x86_32'
  product platform: 'windows', arch: 'x86_64'
  archiveProducts = true
}
```

### Create "settings.gradle"

Create "settings.gradle" in "tutorials" folder (parent of "MySwtApp" folder), insert code:

```groovy
include 'MySwtApp'
```

### Compile

Invoke on command line in "tutorials" folder: `gradle build`.

Check: build task must generate products in "tutorials/MySwtApp/build/output" folder.

---

The example code for this page: [tutorialExamples/SwtApp-3](../tree/master/tutorialExamples/SwtApp-3).

Next page: [Create Eclipse bundle and use it in SWT app](Create-Eclipse-bundle-and-use-it-in-SWT-app).