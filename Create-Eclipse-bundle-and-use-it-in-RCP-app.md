We already [prepared RCP app for multiproject build](Prepare-RCP-app-for-multiproject-build). Now we create Eclipse plugin and use it in RCP app.

### Create Eclipse bundle

Create folder "tutorials/MyPlugin", create file "build.gradle" in it, insert code:

```groovy
apply plugin: 'java'
apply plugin: 'org.akhikhl.wuff.eclipse-bundle'
```

Create folder "tutorials/MyPlugin/src/main/java/myplugin", create file "HelloWorld.java" in it, insert code:

```java
package myplugin;

import org.eclipse.jface.dialogs.MessageDialog;
import org.eclipse.swt.widgets.Shell;

public class HelloWorld {

  public static void showMessageDialog(Shell shell) {
    MessageDialog.openInformation(shell, "Information", "I am Eclipse plugin!");
  }
}
```

Edit file "tutorials/settings.gradle", insert code:

```groovy
include 'MyPlugin'
```
so that there are two includes - "MyRcpApp" and "MyPlugin".

### Use Eclipse bundle in RCP app

Edit file "tutorials/MyRcpApp/build.gradle", insert code:

```groovy
dependencies {
  compile project(':MyPlugin')
}
```

Edit file "tutorials/MyRcpApp/src/main/java/myrcpapp/View.java", replace content with:

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
        myplugin.HelloWorld.showMessageDialog(parent.getShell());
      }
    });
  }

  @Override
  public void setFocus() {
  }
}
```

### Compile

Invoke on command line in "tutorials" folder: `gradle build`

Check: folder "tutorials/MyPlugin/build/libs" must contain file "MyPlugin-1.0.0.0.jar", which is proper OSGi bundle with automatically generated manifest.

Check: each product in "tutorials/MyRcpApp/build/output" must contain "MyPlugin" and "MyRcpApp" bundles in "plugins" subfolder and in "configuration/config.ini". 

### Run

Run the compiled product from command line. Expect to see:
 
![RcpApp-4-run-1](images/RcpApp-4-run-1.png "RcpApp-4-run-1")

When we click on "Show dialog" button, the program shows message dialog:

![RcpApp-4-run-2](images/RcpApp-4-run-2.png "RcpApp-4-run-2")

---

The example code for this page: [examples/RcpApp-4](../tree/master/examples/RcpApp-4).

Next page: [add splash to RCP app](Add-splash-to-RCP-app).
