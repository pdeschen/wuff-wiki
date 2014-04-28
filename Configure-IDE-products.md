We already [created first IDE app](Create-first-IDE-app). Now we configure IDE products.

### Create product definitions

Edit the file "tutorials/MyIdeApp/build.gradle", insert code:

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

### Compile

Invoke on command line: `gradle build`.

Check: there must be 4 products in "tutorials/MyIdeApp/build/output" folder. 

Check: each product must contain "MyIdeApp" bundle in "plugins" subfolder and in "configuration/config.ini".

### Run

We can run each product on corresponding OS and architecture. On Windows platform we start application via .bat-file, on other platforms we start application via .sh-file.

Attention: do not try to run the generated product on a "wrong" OS or "wrong" architecture. 
If you are on Windows, Linux product won't start. If your JRE is 32-bit, 64-bit product won't start.

---

The example code for this page: [examples/IdeApp-2](../tree/master/examples/IdeApp-2).

Next page: [Prepare IDE app for multiproject build](Prepare-IDE-app-for-multiproject-build).