We already [added intro page to RCP app](Add-intro-page-to-RCP-app). Now we localize RCP app.

1. Let's add language-specific product definitions to "build.gradle":

  ```groovy
  products {
    product platform: 'linux', arch: 'x86_32'
    product platform: 'linux', arch: 'x86_32', language: 'de'
    product platform: 'linux', arch: 'x86_64'
    product platform: 'linux', arch: 'x86_64', language: 'de'
    product platform: 'windows', arch: 'x86_32'
    product platform: 'windows', arch: 'x86_32', language: 'de'
    product platform: 'windows', arch: 'x86_64'
    product platform: 'windows', arch: 'x86_64', language: 'de'
    archiveProducts = true
  }
  ```

  Here we define 8 products: 4 are English, 4 are German.

2. Edit file "tutorials/MyRcpApp/src/main/java/myrcpapp/View.java", replace content with:

  ```java
  package myrcpapp;

  import java.util.Locale;
  import java.util.ResourceBundle;

  import org.eclipse.swt.SWT;
  import org.eclipse.swt.widgets.Composite;
  import org.eclipse.swt.events.SelectionAdapter;
  import org.eclipse.swt.events.SelectionEvent;
  import org.eclipse.swt.layout.RowLayout;
  import org.eclipse.swt.widgets.Button;
  import org.eclipse.ui.part.ViewPart;

  public class View extends ViewPart {

    private static ResourceBundle res = ResourceBundle.getBundle(View.class.getName(), Locale.getDefault());

    @Override
    public void createPartControl(final Composite parent) {
      parent.setLayout(new RowLayout());
      Button btnShowDialog = new Button(parent, SWT.PUSH);
      btnShowDialog.setText(res.getString("btnShowDialog_Label"));
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

3. Create folder "tutorials/MyRcpApp/src/main/resources/myrcpapp", create file "View.properties" in it, insert content:

```
btnShowDialog_Label=Show dialog
```

4. Create file "View_de.properties" in the same folder, insert content:

```
btnShowDialog_Label=Dialogfenster anzeigen
```
