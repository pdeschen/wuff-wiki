We already [created IDE bundle and used it in IDE app](Create-IDE-bundle-and-use-it-in-IDE-app). Now we add perspective and view to IDE app.

### Create view

Create folder "tutorials/MyIdeApp/src/main/java/myideapp", create file "View.java" in it, insert code:

```java
package myideapp;

import org.eclipse.jface.dialogs.MessageDialog;
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
        MessageDialog.openInformation(parent.getShell(), "Message", "There is no spoon.");
      }
    });
  }

  @Override
  public void setFocus() {
  }
}
```

### Create perspective

Create file "tutorials/MyIdeApp/src/main/java/myideapp/Perspective.java", insert code:

```java
package myideapp;

import org.eclipse.ui.IPageLayout;
import org.eclipse.ui.IPerspectiveFactory;

public class Perspective implements IPerspectiveFactory {

  public void createInitialLayout(IPageLayout layout) {
	  layout.setEditorAreaVisible(false);
  }
}
```

### Compile

Invoke on command line in "tutorials/MyIdeApp" folder: `gradle clean build`.

Hint: "clean" is needed only once, as soon as we introduced view or perspective. This way we remove cached information on IDE layout, that is stored in "configuration" subfolder of compiled product. Consequent builds can be done without "clean".

Note that we don't have to configure view and perspective in "plugin.xml": Wuff does this automatically. More concretely: when Wuff recognizes that an application contains only one perspective and one view, it decides, that the perspective should open on startup and contain exactly this one view.

### Run

Run the compiled product from command line. As soon as program is fully started, you see new perspective and view with button:

![IdeApp-5-run-1](images/IdeApp-5-run-1.png "IdeApp-5-run-1")

When you click the button, the program shows message dialog:

![IdeApp-5-run-2](images/IdeApp-5-run-2.png "IdeApp-5-run-2")

### Rename perspective

You see on the perspective button: "MyIdeApp Perspective". Wuff generated this label for you automatically. Let's rename the perspective to something else, for example, to "la vista". Create file "tutorials/MyIdeApp/src/main/resources/plugin.xml", insert code:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<?eclipse version="3.4"?>
<plugin>
  <extension point="org.eclipse.ui.perspectives">
    <perspective id="MyIdeApp.VistaPerspective" name="la vista" class="myideapp.Perspective"/>
  </extension>
</plugin>
```

then do "gradle clean build" and start the product. Now perspective has proper label:

![IdeApp-5-run-3](images/IdeApp-5-run-3.png "IdeApp-5-run-3")

The chapter [plugin.xml for eclipse-bundle](plugin.xml-for-eclipse-bundle) contains more information on customizing views and perspectives.

---

The example code for this page: [examples/IdeApp-5](../tree/master/examples/IdeApp-5).

Next page: [Add splash to IDE app](Add-splash-to-IDE-app).