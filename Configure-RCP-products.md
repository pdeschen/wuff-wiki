We already [created first RCP app](Create-first-RCP-app). Now we configure RCP products.

### Add product definitions

Edit the file "build.gradle", insert code:

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

Check: there must be 4 products in "tutorials/MyRcpApp/build/output" folder.

Check: each product must contain "MyRcpApp" bundle in "plugins" subfolder and in "configuration/config.ini". 

### Run

We can run each product on corresponding OS and architecture. On Windows platform we start application via .bat-file, on other platforms we start application via .sh-file.

Attention: do not try to run the generated product on a "wrong" OS or "wrong" architecture. 
Linux product won't start on Windows. 64-bit product won't start on 32-bit JRE.

---

The example code for this page: [examples/RcpApp-2](../tree/master/examples/RcpApp-2).

Next page: [Prepare RCP app for multiproject build](Prepare-RCP-app-for-multiproject-build).