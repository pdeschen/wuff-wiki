Let's create eclipse bundle and program "plugin.xml" for it.

1. Create folder "tutorials/MyEclipseplugin", create file "build.gradle" in it, insert code:

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
  apply plugin: 'eclipse-bundle'

  repositories {
    mavenLocal()
    jcenter()
  }
  ```

2. Invoke on command line: `build gradle`

3. Open file "tutorials/MyEclipsePlugin/build/libs/MyEclipsePlugin-1.0.0.0.jar" - it does not contain "plugin.xml". Explanation: Wuff skips default "plugin.xml" generation, because it does not "know" what to write there.

4. Create folder "tutorials/MyEclipsePlugin/src/main/java/myeclipseplugin", create file "MyView.java" in it, insert code:

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

5. Invoke on command line: `build gradle`

6. Open file "tutorials/MyEclipsePlugin/build/libs/MyEclipsePlugin-1.0.0.0.jar" - it contains "plugin.xml" with the following code:

  ```xml
  <plugin>
    <extension point="org.eclipse.ui.views">
      <view id="MyEclipsePlugin.MyView" name="MyEclipsePlugin MyView" class="myeclipseplugin.MyView"/>
    </extension>
  </plugin>
  ```

  We see that Wuff recognized our file as view and that it automatically inserted extension-point for it. In general, Wuff recognizes any files matching to patterns `'**/*View.groovy', '**/*View.java', '**/View*.groovy', '**/View*.java'` as view files.

  Explanation of attributes:
  - id="MyEclipsePlugin.MyView": id was synthesized from project name and view class name
  - name="MyEclipsePlugin MyView": name was synthesized from project name and view class name
  - class="myeclipseplugin.MyView": class points to qualified class name of the found view file.

7. What should we do to change the view name? Very simple: give our own view definition. Create folder "tutorials/MyEclipsePlugin/src/main/resources", create file "plugin.xml" in it, insert code: