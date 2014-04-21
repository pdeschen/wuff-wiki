Let's build equinox application with wuff. Our prerequisites: JDK, gradle and access to jcenter.

1. Create new folder, create file "build.gradle" in it, insert code:

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
  apply plugin: 'eclipse-equinox-app'

  repositories {
    mavenLocal()
    jcenter()
  }
  ```

  The script describes that we are using wuff gradle-plugin
  and that we apply "eclipse-equinox-app" plugin to this project.

2. Invoke on command line:

  ```shell
  gradle scaffold
  ```

  Scaffold task creates Application class required by equinox library.

3. Invoke on command line:

  ```shell
  gradle build
  ```

  Build task generates product in "build/output" folder.

4. You can run the program either by invoking launch script within the product or by invoking "gradle run" 
  in project's directory. When you run the program, it prints to stdout:
  
  *Hello, world! I am equinox application!*

5. Now let's add product definitions to "build.gradle":
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

6. Repeat steps (3) and (4), see how products are generated "build/output".

  **Attention:** do not try to run the generated product on a "wrong" OS or "wrong" architecture. 
  If you are on Windows, Linux product won't start. If your JRE is 32-bit, 64-bit product won't start.