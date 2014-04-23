In this tutorial we start from scratch and build Eclipse IDE app. Other tutorials are available [here](Tutorials).

1. Create folder "tutorials/MyIdeApp", create file "build.gradle" in it, insert code:

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
  apply plugin: 'eclipse-ide-app'

  repositories {
    mavenLocal()
    jcenter()
  }
  ```
