In this tutorial we show how to build Eclipse RCP application with wuff.

1. Create folder "tutorials/MyRcpApp", create file "build.gradle" in it, insert code:

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
  apply plugin: 'eclipse-rcp-app'

  repositories {
    mavenLocal()
    jcenter()
  }
  ```

  The script describes that we are using wuff gradle-plugin and that we apply "eclipse-rcp-app" plugin to this project.

2. Invoke on command line:

  ```shell
  gradle scaffold
  ```

  Scaffold task creates classes required by Eclipse RCP.

3. Invoke on command line:

  ```shell
  gradle build
  ```

  Build task generates product in "build/output" folder.

  Note that you don't have to program "plugin.xml", "MANIFEST.MF", "config.ini" - all these files are generated and inserted into bundle and product automatically.

  **Attention:** first build is slow, because wuff will download Eclipse and install it's bundles into local maven repository ($HOME/.m2/repository). Consequent builds will be much faster.

  **CHECK:** folder "tutorials/MyRcpApp/build/libs" contains file "MyRcpApp-1.0.0.0.jar", which is proper OSGi bundle with automatically generated manifest and "plugin.xml".

  **CHECK:** There's one product in "tutorials/MyEquinoxApp/build/output" folder. It contains "MyRcpApp" bundle in "plugins" subfolder and in "configuration/config.ini". 

  **CHECK:** The product is runnable and shows window with title "Hello, RCP".
