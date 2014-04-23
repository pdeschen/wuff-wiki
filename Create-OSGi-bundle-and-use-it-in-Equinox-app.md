We already [prepared Equinox app for multiproject build](Prepare-Equinox-app-for-multiproject-build). Now we create OSGi-bundle and use it in Equinox app.

1. Create folder "tutorials/MyBundle", create file "build.gradle" in it, insert code:

  ```groovy
  apply plugin: 'java'
  apply plugin: 'osgi-bundle'
  ```

2. Create folder "tutorials/MyBundle/src/main/java/mybundle", create file "HelloWorld.java" in it, insert code:

  ```java
  package mybundle;

  public class HelloWorld {

    public static void sayHello() {
      System.out.println("Hello, world!");
    }
  }
  ```

3. Edit file "tutorials/settings.gradle", insert code:

  ```groovy
  include 'MyBundle'
  ```
  so that there are two includes - "MyEquinoxApp" and "MyBundle".

4. Edit file "tutorials/MyEquinoxApp/build.gradle", insert code:

  ```groovy
  dependencies {
    compile project(':MyBundle')
  }
  ```

5. Edit file "tutorials/MyEquinoxApp/src/main/java/myequinoxapp/Application.java", replace line containing `System.out.println` with `mybundle.HelloWorld.sayHello();` so that the file looks like this:

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

6. Invoke on command line in "tutorials" folder:
  ```shell
  gradle build
  ```

  **CHECK:** folder "tutorials/MyBundle/build/libs" contains file "MyBundle-1.0.0.0.jar", which is proper OSGi bundle with automatically generated manifest.

  **CHECK:** Each product in "tutorials/MyEquinoxApp/build/output" contains "MyBundle" and "MyEquinoxApp" bundles in "plugins" subfolder and in "configuration/config.ini". 

  **CHECK:** Each generated product is runnable on corresponding OS and architecture. Upon run, it prints "Hello, world!" to the console.

The example code for this page: [tutorialExamples/EquinoxApp-4](../tree/master/tutorialExamples/EquinoxApp-4).

Now we are done with Equinox tutorial. Other tutorials are available [here](Tutorials).
