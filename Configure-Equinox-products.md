We already [created first Equinox app](Create-first-Equinox-app). Now we configure Equinox products.

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

  **CHECK:** There are 4 products in "tutorials/MyEquinoxApp/build/output" folder. Each product contains "MyEquinoxApp" bundle in "plugins" subfolder and in "configuration/config.ini". 

  **CHECK:** Each generated product is runnable on corresponding OS and architecture.

  **Attention:** do not try to run the generated product on a "wrong" OS or "wrong" architecture. 
  Linux product won't start on windows. 64-bit product won't start on 32-bit JRE.

The example code for this page: [tutorialExamples/EquinoxApp-2](../tree/master/tutorialExamples/EquinoxApp-2).

Next page: [Prepare Equinox app for multiproject build](Prepare-Equinox-app-for-multiproject-build).