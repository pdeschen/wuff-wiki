Repeat steps (1) and (2) from [First equinox app](First-equinox-app), then do the following:

3. Edit the file "build.gradle", insert at the end:
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

4. Invoke on command line:
  ```shell
  gradle build
  ```
  Build task generates product in "build/output" folder.

5. You can run the program either by invoking launch script within the product or by invoking "gradle run" 
  in project's directory. When you run the program, it prints to stdout:
  
  *Hello, world! I am equinox application!*

**Attention:** do not try to run the generated product on a "wrong" OS or "wrong" architecture. If you are on Windows, Linux product won't start. If your JRE is 32-bit, 64-bit product won't start.