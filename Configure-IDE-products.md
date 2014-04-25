We already [created first IDE app](Create-first-IDE-app). Now we configure IDE products.

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

2. Invoke on command line: `gradle build`

  **CHECK:** There are 4 products in "tutorials/MyIdeApp/build/output" folder. Each product contains "MyIdeApp" bundle in "plugins" subfolder and in "configuration/config.ini". 

  **CHECK:** Each generated product is runnable on corresponding OS and architecture.

  **Attention:** do not try to run the generated product on a "wrong" OS or "wrong" architecture. 
  If you are on Windows, Linux product won't start. If your JRE is 32-bit, 64-bit product won't start.

The example code for this page: [tutorialExamples/IdeApp-2](../tree/master/tutorialExamples/IdeApp-2).

Next page: [Prepare IDE app for multiproject build](Prepare-IDE-app-for-multiproject-build).