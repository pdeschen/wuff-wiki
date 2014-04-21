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

6. Now let's create Eclipse bundle and use it in RCP application. First, we reorganize "MyRcpApp" for multi-project build:

  6.1. Create "build.gradle" in "tutorials" folder (parent of "MyRcpApp" folder) 

  6.2. Move "buildscript" and "repositories" from "tutorials/MyRcpApp/build.gradle" to "tutorials/build.gradle", so that two scripts look like this:

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

    "tutorials/MyRcpApp/build.gradle":
    ```groovy
    apply plugin: 'java'
    apply plugin: 'eclipse-rcp-app'
      
    products {
      product platform: 'linux', arch: 'x86_32'
      product platform: 'linux', arch: 'x86_64'
      product platform: 'windows', arch: 'x86_32'
      product platform: 'windows', arch: 'x86_64'
      archiveProducts = true
    }
    ```

  6.3. Create "settings.gradle" in "tutorials" folder (parent of "MyRcpApp" folder), insert code:

    ```groovy
    include 'MyRcpApp'
    ```

7. Create folder "tutorials/MyBundle", create file "build.gradle" in it, insert code:

  ```groovy
  apply plugin: 'java'
  apply plugin: 'eclipse-bundle'
  ```

8. Create folder "tutorials/MyBundle/src/main/java/mybundle", create file "HelloWorld.java" in it, insert code:

  ```java
  package mybundle;

  import org.eclipse.jface.dialogs.MessageDialog;
  import org.eclipse.swt.widgets.Shell;

  public class HelloWorld {

    public static void showMessageDialog(Shell shell) {
      MessageDialog.openQuestion(shell, "Information", "Hello, world!");
    }
  }
  ```

9. Edit file "tutorials/settings.gradle", insert code:

  ```groovy
  include 'MyBundle'
  ```
  so that there are two includes - "MyRcpApp" and "MyBundle".

10. Edit file "tutorials/MyRcpApp/build.gradle", insert code:

  ```groovy
  dependencies {
    compile project(':MyBundle')
  }
  ```

11. Edit file "tutorials/MyRcpApp/src/main/java/myrcpapp/View.java", replace content to:

  ```groovy
  package myrcpapp;

  import org.eclipse.swt.SWT;
  import org.eclipse.swt.widgets.Composite;
  import org.eclipse.swt.events.SelectionAdapter;
  import org.eclipse.swt.events.SelectionEvent;
  import org.eclipse.swt.layout.RowLayout;
  import org.eclipse.swt.widgets.Button;
  import org.eclipse.ui.part.ViewPart;

  public class View extends ViewPart {

    @Override
    public void createPartControl(final Composite parent) {
      parent.setLayout(new RowLayout());
      Button btnShowDialog = new Button(parent, SWT.PUSH);
      btnShowDialog.setText("Show dialog");
      btnShowDialog.addSelectionListener(new SelectionAdapter() {
        @Override
        public void widgetSelected(SelectionEvent event) {
          mybundle.HelloWorld.showMessageDialog(parent.getShell());
        }
      });
    }

    @Override
    public void setFocus() {
    }
  }
  ```