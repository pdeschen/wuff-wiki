In this tutorial we start from scratch and build RCP app. Other tutorials are available [here](Tutorials).

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

  **CHECK:** folder "tutorials/MyRcpApp/build/libs" contains file "MyRcpApp-1.0.0.0.jar", which is proper OSGi bundle with automatically generated manifest and "plugin.xml".

  **CHECK:** There's one product in "tutorials/MyEquinoxApp/build/output" folder. It contains "MyRcpApp" bundle in "plugins" subfolder and in "configuration/config.ini". 

  **Attention:**  first build is slow, because wuff downloads Eclipse and installs it's bundles into local maven repository ($HOME/.m2/repository). Consequent builds will be much faster.

  Note that you don't have to program "plugin.xml", "MANIFEST.MF", "config.ini" - all these files are generated and inserted into bundle and product automatically.
  
4. Run the compiled product from command line. The expected output:
   
   ![RcpApp-1-run-1](images/RcpApp-1-run-1.png "RcpApp-1-run-1")

The example code for this page: [tutorialExamples/RcpApp-1](../tree/master/tutorialExamples/RcpApp-1).

Next page: [Configure RCP products](Configure-RCP-products).