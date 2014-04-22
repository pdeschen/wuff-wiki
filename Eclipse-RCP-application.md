6. Now let's create Eclipse bundle and use it in RCP application. 

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

11. Edit file "tutorials/MyRcpApp/src/main/java/myrcpapp/View.java", replace content with:

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

12. Invoke on command line in "tutorials" folder:
  ```shell
  gradle build
  ```

  **CHECK:** folder "tutorials/MyBundle/build/libs" contains file "MyBundle-1.0.0.0.jar", which is proper OSGi bundle with automatically generated manifest.

  **CHECK:** Each product in "tutorials/MyRcpApp/build/output" contains "MyBundle" and "MyRcpApp" bundles in "plugins" subfolder and in "configuration/config.ini". 

  **CHECK:** The product matching your OS/architecture is runnable and shows window with title "Hello, RCP" and with button "Show dialog". When you click the button, the program shows modal dialog with text "Hello, world!".