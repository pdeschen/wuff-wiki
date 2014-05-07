Conversion of existing Eclipse plugins and apps to Gradle is very easy, when we apply Wuff. The Eclipse projects themselves do not need to be restructured or even facilitated with "build.gradle" - Wuff does all work for us.

Lets try the following simple scenario: we create two Eclipse projects: one is plugin with a view, another is RCP app using the plugin. Then we convert these two to Gradle, using Wuff.

First three parts of this tutorial are done in Eclipse IDE, the last part - in file explorer and console.

### Create Eclipse plugin project

1. Invoke menu "File/New/Project...", New Wizard dialog pops up.
2. Select "Plug-in Project", click "Next".
3. Enter project name "MyPlugin", leave all other fields default, click "Next".
4. Choose whatever name and ID for project, make sure that "Rich Client Application" is set to "No", click "Next".
5. Choose template "Plug-in with a view", click "Next".
6. Choose whatever package and class names, view category. Click "Finish".

### Create Eclipse RCP app project

1. Invoke menu "File/New/Project...", New Wizard dialog pops up.
2. Select "Plug-in Project", click "Next".
3. Enter project name "MyRcpApp", leave all other fields default, click "Next".
4. Choose whatever name and ID for project, make sure that "Rich Client Application" is set to "Yes", click "Next".
5. Choose template "Hello RCP", click "Next".
6. Choose whatever package and class names, click "Finish".

### Use plugin in RCP app

1. Double-click "MyRcpApp/META-INF/MANIFEST.MF", switch to tab "Dependencies".
2. Click "Add", "Plug-in Selection" dialog appears. Enter symbolic name of the Eclipse plugin we created previously ("MyPlugin", if symbolic name wasn't changed). Click "OK".
3. Save manifest (Ctrl+S).
4. Switch to "plugin.xml" tab, insert fragment:

  ```xml
  <extension point="org.eclipse.ui.perspectiveExtensions">
    <perspectiveExtension targetID="*">
      <view standalone="true"
        minimized="false"
        relative="org.eclipse.ui.editorss"
        relationship="left"
        id="myplugin.views.SampleView">
      </view>
    </perspectiveExtension>
  </extension>
  ```
5. Save "plugin.xml" (Ctrl+S).