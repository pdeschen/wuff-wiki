We already learned what [default "plugin.xml"](Default-plugin.xml) is. Now we will program "plugin.xml" for Eclipse bundle.

### Create "build.gradle"

Create folder "tutorials/MyEclipseplugin", create file "build.gradle" in it, insert code:

```groovy
buildscript {
  repositories {
    mavenLocal()
    jcenter()
  }

  dependencies {
    classpath 'org.akhikhl.wuff:wuff-plugin:+'
  }
}

apply plugin: 'java'
apply plugin: 'eclipse-bundle'

repositories {
  mavenLocal()
  jcenter()
}
```

### Compile and inspect default "plugin.xml"

Invoke on command line: `build gradle`.

Open file "tutorials/MyEclipsePlugin/build/libs/MyEclipsePlugin-1.0.0.0.jar" - it does not contain "plugin.xml". Explanation: Wuff skips default "plugin.xml" generation, because it does not "know" what to write there. Particularly, our project does not contain views or perspectives to be registered in default "plugin.xml".

### Create view

Create folder "tutorials/MyEclipsePlugin/src/main/java/myeclipseplugin", create file "MyView.java" in it, insert code:

```java
package myeclipseplugin;

import org.eclipse.swt.widgets.Composite;
import org.eclipse.ui.part.ViewPart;

public class MyView extends ViewPart {

  @Override
  public void createPartControl(final Composite parent) {
  }

  @Override
  public void setFocus() {
  }
}
```

### Compile and inspect default view extension-point

Invoke on command line: `build gradle`.

Open file "tutorials/MyEclipsePlugin/build/libs/MyEclipsePlugin-1.0.0.0.jar" - it contains "plugin.xml" with the following content:

```xml
<plugin>
  <extension point="org.eclipse.ui.views">
    <view id="MyEclipsePlugin.MyView" name="MyEclipsePlugin MyView" class="myeclipseplugin.MyView"/>
  </extension>
</plugin>
```

We see that Wuff recognized our file as a view and that it automatically inserted extension-point for it. In general, Wuff recognizes any files matching to patterns `'**/*View.groovy', '**/*View.java', '**/View*.groovy', '**/View*.java'` as view files and inserts extension-point "org.eclipse.ui.views" for each of them.

Explanation of attributes:
- id="MyEclipsePlugin.MyView": can be any string, was assigned to concatenation of project name and view class name.
- name="MyEclipsePlugin MyView": can be any string, was assigned to concatenation of project name and view class name.
- class="myeclipseplugin.MyView": must be a QCN of the view class.

### Customize view extension-point

What should we do to change the view name or view id? Very simple: give our own view definition. Create folder "tutorials/MyEclipsePlugin/src/main/resources", create file "plugin.xml" in it, insert content:

```xml
<plugin>
  <extension point="org.eclipse.ui.views">
    <view id="myviewid" name="Very nice view" class="myeclipseplugin.MyView"/>
  </extension>
</plugin>
```

### Compile and inspect custom view extension-point

Invoke on command line: `build gradle`.

Open file "tutorials/MyEclipsePlugin/build/libs/MyEclipsePlugin-1.0.0.0.jar" - it contains "plugin.xml" with our view extension-point, not the default one.

### Create perspective

Create file "tutorials/MyEclipsePlugin/src/main/java/myeclipseplugin/MyPerspective.java", insert code:

```java
package myeclipseplugin;

import org.eclipse.ui.IPageLayout;
import org.eclipse.ui.IPerspectiveFactory;

public class MyPerspective implements IPerspectiveFactory {

  public void createInitialLayout(IPageLayout layout) {
  }
}
```

### Compile and inspect default perspective extension-point

Invoke on command line: `build gradle`.

Open file "tutorials/MyEclipsePlugin/build/libs/MyEclipsePlugin-1.0.0.0.jar" - it contains "plugin.xml" with the following content:

```xml
<plugin>
  <extension point="org.eclipse.ui.views">
    <view id="myviewid" name="Very nice view" class="myeclipseplugin.MyView"/>
  </extension>
  <extension point="org.eclipse.ui.perspectives">
    <perspective id="MyEclipsePlugin.MyPerspective" name="MyEclipsePlugin MyPerspective" class="myeclipseplugin.MyPerspective"/>
  </extension>
  <extension point="org.eclipse.ui.perspectiveExtensions">
    <perspectiveExtension targetID="MyEclipsePlugin.MyPerspective">
      <view id="myviewid" standalone="true" minimized="false" relative="org.eclipse.ui.editorss" relationship="left"/>
    </perspectiveExtension>
  </extension>
</plugin>
```

We see that Wuff recognized "MyPerspective.java" file as a perspective and that it automatically inserted extension-points for it. In general, Wuff recognizes any files matching to patterns `'**/*Perspective.groovy', '**/*Perspective.java', '**/Perspective*.groovy', '**/Perspective*.java'` as perspective files and inserts extension point "org.eclipse.ui.perspectives" for each of them.

Explanation of attributes in "org.eclipse.ui.perspectives":
- id="MyEclipsePlugin.MyPerspective": can be any string, was assigned to concatenation of project name and perspective class name.
- name="MyEclipsePlugin MyPerspective": can be any string, was assigned to concatenation of project name and perspective class name.
- class="myeclipseplugin.MyPerspective": must be a QCN of the perspective class.

As we see, extension-point "org.eclipse.ui.perspectiveExtensions" links perspective and view. This is special case: our plugin contains exactly one perspective and one view, so Wuff decides that they must be linked to each other.

### Customize perspective extension-point

Let's customize our perspective as well. Edit the file "tutorials/MyEclipsePlugin/src/main/resources/plugin.xml", insert content:

```xml
<plugin>
  <extension point="org.eclipse.ui.views">
    <view id="myviewid" name="Very nice view" class="myeclipseplugin.MyView"/>
  </extension>
  <extension point="org.eclipse.ui.perspectives">
    <perspective id="myperspectiveid" name="Very nice perspective" class="myeclipseplugin.MyPerspective"/>
  </extension>
</plugin>
```
### Compile and inspect custom perspective extension-point

Invoke on command line: `build gradle`.

Open file "tutorials/MyEclipsePlugin/build/libs/MyEclipsePlugin-1.0.0.0.jar" - it contains "plugin.xml" with the following content:

```xml
<plugin>
  <extension point="org.eclipse.ui.views">
    <view id="myviewid" name="Very nice view" class="myeclipseplugin.MyView"/>
  </extension>
  <extension point="org.eclipse.ui.perspectives">
    <perspective id="myperspectiveid" name="Very nice perspective" class="myeclipseplugin.MyPerspective"/>
  </extension>
  <extension point="org.eclipse.ui.perspectiveExtensions">
    <perspectiveExtension targetID="myperspectiveid">
      <view id="myviewid" standalone="true" minimized="false" relative="org.eclipse.ui.editorss" relationship="left"/>
    </perspectiveExtension>
  </extension>
</plugin>
```

As we see, now Wuff recognizes that "plugin.xml" already contains extension-point for perspective and does not generate the default one. We also see that Wuff still links perspective and view, because it is a special case: one perspective and one view.

---

The example code for this page: [examples/PluginXml-1](../tree/master/examples/PluginXml-1) and [examples/PluginXml-2](../tree/master/examples/PluginXml-2).

Next page: ["plugin.xml" for Equinox app](Plugin.xml-for-eclipse-equinox-app).