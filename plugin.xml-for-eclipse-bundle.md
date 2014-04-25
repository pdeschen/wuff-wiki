Let's create eclipse bundle and program "plugin.xml" for it.

1. Create folder "tutorials/MyEclipseplugin", create file "build.gradle" in it, insert code:

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

  apply plugin: 'java'
  apply plugin: 'eclipse-bundle'

  repositories {
    mavenLocal()
    jcenter()
  }
  ```

2. Invoke on command line: ```build gradle```