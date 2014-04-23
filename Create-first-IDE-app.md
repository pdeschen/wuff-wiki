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

2. Invoke on command line:

  ```shell
  gradle build
  ```

  **CHECK:** folder "tutorials/MyIdeApp/build/libs" contains file "MyIdeApp-1.0.0.0.jar", which is proper OSGi bundle with automatically generated manifest and "plugin.xml".

  **CHECK:** There's one product in "tutorials/MyIdeApp/build/output" folder. It contains "MyIdeApp" bundle in "plugins" subfolder and in "configuration/config.ini". 

  **Attention:**  first build is slow, because wuff downloads Eclipse and installs it's bundles into local maven repository ($HOME/.m2/repository). Consequent builds will be much faster.

  Note that you don't have to program "plugin.xml", "MANIFEST.MF", "config.ini" - all these files are generated and inserted into bundle and product automatically. It's not even necessary to write any java code - you need only "build.gradle" and that's it.