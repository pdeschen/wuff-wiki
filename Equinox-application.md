Let's build equinox application with wuff.

1. Create new folder "tutorials/MyEquinoxApp", create file "build.gradle" in it, insert code:

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

  Note that you don't have to program "plugin.xml", "MANIFEST.MF", "config.ini" - all these files are generated and inserted into bundle and product automatically.

  **Attention:** first build make time some time, because wuff will download Eclipse and install it's bundles into local maven repository ($HOME/.m2/repository). Consequent builds will be much faster.

4. You can run the program either by invoking launch script (.bat or .sh, depending on OS) within the product or by invoking "gradle run" in project's directory. When you run the program, it prints to stdout:
  
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

6. Repeat steps (3) and (4), see which products are generated in "build/output".

  **Attention:** do not try to run the generated product on a "wrong" OS or "wrong" architecture. 
  If you are on Windows, Linux product won't start. If your JRE is 32-bit, 64-bit product won't start.

7. Now let's create OSGi bundle and use it in equinox application. First, we reorganize "MyEquinoxApp" for multi-project build:

  7.1. Create "build.gradle" in "tutorials" folder (parent of "MyEquinoxApp" folder) 

  7.2. Move "buildscript" and "repositories" from "tutorials/MyEquinoxApp/build.gradle" to "tutorials/build.gradle", so that two scripts look like this:

    "tutorials/build.gradle":
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

    subprojects {
      repositories {
        mavenLocal()
        jcenter()
      }
    }
    ```

    "tutorials/MyEquinoxApp/build.gradle":
    ```groovy
    apply plugin: 'java'
    apply plugin: 'eclipse-equinox-app'
      
    products {
      product platform: 'linux', arch: 'x86_32'
      product platform: 'linux', arch: 'x86_64'
      product platform: 'windows', arch: 'x86_32'
      product platform: 'windows', arch: 'x86_64'
      archiveProducts = true
    }
    ```

  7.3. Create "settings.gradle" in "tutorials" folder (parent of "MyEquinoxApp" folder), insert code:

    ```groovy
    include 'MyEquinoxApp'
    ```

8. Create new folder "tutorials/MyBundle", create file "build.gradle" in it, insert code:

  ```groovy
  apply plugin: 'java'
  apply plugin: 'osgi-bundle'
  ```

9. Create subfolder "src/main/java/mybundle", create file "HelloWorld.java" in it, insert code:

  ```java
  package mybundle;

  public class HelloWorld {

    public static void sayHello() {
      System.out.println("Hello, world!");
    }
  }
  ```

10. Edit file "tutorials/settings.gradle", insert code:

  ```groovy
  include 'MyBundle'
  ```
  so that there are two includes - "MyEquinoxApp" and "MyBundle".

11. Edit file "tutorials/MyEquinoxApp/build.gradle", insert code:

  ```groovy
  dependencies {
    compile project(':MyBundle')
  }
  ```

12. Edit file "tutorials/MyEquinoxApp/src/main/java/myequinoxapp/Application.java", replace line containing `System.out.println` with `mybundle.HelloWorld.sayHello();` so that the file looks like this:

  ```java
  package myequinoxapp;

  import java.io.IOException;

  import org.eclipse.equinox.app.IApplication;
  import org.eclipse.equinox.app.IApplicationContext;

  public class Application implements IApplication {

    @Override
    public Object start(IApplicationContext ctx) throws Exception {
      mybundle.HelloWorld.sayHello();
      return IApplication.EXIT_OK;
    }

    @Override
    public void stop() {
      // From eclipse doc:
      // This method will not be called if an application exits normally from the start(IApplicationContext) method. 
    }
  }
  ```

9. Invoke on command line in "tutorials" folder:
  ```shell
  gradle build
  ```

  **CHECK:** folder "tutorials/MyBundle/build/libs" contains file "MyBundle-1.0.0.0.jar", which is proper OSGi bundle with automatically generated manifest.

  **CHECK:** Each product in "tutorials/MyEquinoxApp/build/output" contains "MyBundle" and "MyEquinoxApp" bundles in "plugins" subfolder. 

  **CHECK:** Each product is runnable and shows "Hello, world!".