We already [prepared IDE app for multiproject build](Prepare-IDE-app-for-multiproject-build). Now we create IDE plugin and use it in IDE app.

1. Create folder "tutorials/MyIdePlugin", create file "build.gradle" in it, insert code:

  ```groovy
  apply plugin: 'java'
  apply plugin: 'eclipse-ide-bundle'

  dependencies {
    compile "${eclipseMavenGroup}:org.eclipse.core.commands:+"
  }
  ```
  We add dependency on org.eclipse.core.commands because we are going to implement menu handler.

2. Create folder "tutorials/MyIdePlugin/src/main/java/myideplugin", create file "MenuHandler.java" in it, insert code:

  ```java
  package myideplugin;

  import org.eclipse.core.commands.AbstractHandler;
  import org.eclipse.core.commands.ExecutionEvent;
  import org.eclipse.core.commands.ExecutionException;
  import org.eclipse.jface.dialogs.MessageDialog;
  import org.eclipse.ui.PlatformUI;

  public final class MenuHandler extends AbstractHandler {

    @Override
    public Object execute(ExecutionEvent event) throws ExecutionException {
      MessageDialog.openQuestion(PlatformUI.getWorkbench().getActiveWorkbenchWindow().getShell(), "Information", "Hello, world!");
      return null;
    }
  }
  ```

3. Edit file "tutorials/settings.gradle", insert code:

  ```groovy
  include 'MyIdePlugin'
  ```
  so that there are two includes - "MyIdeApp" and "MyIdePlugin".

4. Edit file "tutorials/MyIdeApp/build.gradle", insert code:

  ```groovy
  dependencies {
    compile project(':MyIdePlugin')
  }
  ```

5. Edit file "tutorials/MyIdeApp/src/main/java/myideapp/View.java", replace content with:

  ```groovy
  package myideapp;

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
          myideplugin.HelloWorld.showMessageDialog(parent.getShell());
        }
      });
    }

    @Override
    public void setFocus() {
    }
  }
  ```

6. Invoke on command line in "tutorials" folder:
  ```shell
  gradle build
  ```

  **CHECK:** folder "tutorials/MyIdePlugin/build/libs" contains file "MyIdePlugin-1.0.0.0.jar", which is proper OSGi bundle with automatically generated manifest.

  **CHECK:** Each product in "tutorials/MyIdeApp/build/output" contains "MyIdePlugin" and "MyIdeApp" bundles in "plugins" subfolder and in "configuration/config.ini". 
  
4. Run the compiled product from command line. Expect to see:
   
  ![IdeApp-4-run-1](images/IdeApp-4-run-1.png "IdeApp-4-run-1")

  When you click on "Show dialog" button, the program shows message dialog:

  ![IdeApp-4-run-2](images/IdeApp-4-run-2.png "IdeApp-4-run-2")

The example code for this page: [tutorialExamples/IdeApp-4](../tree/master/tutorialExamples/IdeApp-4).

Next page: [add splash to IDE app](Add-splash-to-IDE-app).