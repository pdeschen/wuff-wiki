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

3. Open file "tutorials/MyEclipsePlugin/build/libs/MyEclipsePlugin-1.0.0.0.jar" - it does not contain "plugin.xml". Explanation: Wuff skips default "plugin.xml" generation, because it does not have information on what to write.

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