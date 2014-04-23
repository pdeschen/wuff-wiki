We already [created first RCP app](Create-first-RCP-app). Now we configure RCP products.

1. Let's add product definitions to "build.gradle":

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

2. Invoke on command line:

  ```shell
  gradle build
  ```

  **CHECK:** There are 4 products in "tutorials/MyRcpApp/build/output" folder. Each product contains "MyRcpApp" bundle in "plugins" subfolder and in "configuration/config.ini". 

  **CHECK:** Each generated product is runnable on corresponding OS and architecture. Upon run, it shows window with title "Hello, RCP" and multiline text field with text "Hello, world!".

  **Attention:** do not try to run the generated product on a "wrong" OS or "wrong" architecture. 
  If you are on Windows, Linux product won't start. If your JRE is 32-bit, 64-bit product won't start.

The example code for this page: [tutorialExamples/RcpApp-2](../tree/master/tutorialExamples/RcpApp-2).

Next page: [Prepare RCP app for multiproject build](Prepare-RCP-app-for-multiproject-build).