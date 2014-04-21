In this tutorial we show how to build Eclipse RCP application with wuff.

The compilable examples corresponding to this tutorial are located in [tutorial examples](../tree/master/tutorialExamples).

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

  **Attention:**  first build is slow, because wuff downloads Eclipse and installs it's bundles into local maven repository ($HOME/.m2/repository). Consequent builds will be much faster.

  **CHECK:** folder "tutorials/MyRcpApp/build/libs" contains file "MyRcpApp-1.0.0.0.jar", which is proper OSGi bundle with automatically generated manifest and "plugin.xml".

  **CHECK:** There's one product in "tutorials/MyEquinoxApp/build/output" folder. It contains "MyRcpApp" bundle in "plugins" subfolder and in "configuration/config.ini". 

  **CHECK:** The product is runnable and shows window with title "Hello, RCP".

4. Now let's add product definitions to "build.gradle":

  ```groovy
  products {
    product platform: 'linux', arch: 'x86_32'
    product platform: 'linux', arch: 'x86_64'
    product platform: 'windows', arch: 'x86_32'
    product platform: 'windows', arch: 'x86_64'
    archiveProducts = true
  }
  ```

  Here we define 4 products: 32-bit and 64-bit versions for Linux and 32-bit and 64-bit versions for Windows.
  Optional archiveProducts flag instructs wuff to archive the generated products. Linux versions will be 
  archived as .tar.gz, Windows versions - as .zip. The default value of archiveProducts is false.

5. Repeat steps (3) and (4), see which products are generated in "build/output".

  **CHECK:** There are 4 products in "tutorials/MyEquinoxApp/build/output" folder. Each product contains "MyRcpApp" bundle in "plugins" subfolder and in "configuration/config.ini". 

  **CHECK:** The product matching your OS/architecture is runnable and shows window with title "Hello, RCP".

  **Attention:** do not try to run the generated product on a "wrong" OS or "wrong" architecture. 
  If you are on Windows, Linux product won't start. If your JRE is 32-bit, 64-bit product won't start.
