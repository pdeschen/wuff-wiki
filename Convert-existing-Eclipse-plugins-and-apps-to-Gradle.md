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

### Convert to Gradle

1. Open the directory containing both projects (MyPlugin and MyRcpApp) with a file explorer.
2. Create file "settings.gradle" in that directory, insert code:

  ```groovy
  rootProject.projectDir.listFiles({ new File(it, 'build.properties').isFile() } as FileFilter).each { File subdir ->
    include subdir.absolutePath.substring(rootProject.projectDir.absolutePath.length() + 1).replace(File.separator, ':')
  }
  ```
  Explanation: we organize multi-project build (it could contain not only two, but hundreds of Eclipse projects). The projects are auto-discovered by Gradle: if subdirectory contains file "build.properties" (which is Eclipse-specific), it is considered to be a project.

3. Create file "build.gradle" in the same directory, insert code:
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

  subprojects {

    repositories {
      mavenLocal()
      jcenter()
    }

    apply plugin: 'java'
    if(name == 'MyRcpApp')
      apply plugin: 'eclipse-rcp-app'
    else
      apply plugin: 'eclipse-bundle'
  }
  ```
  Explanation: we configure maven repositories and include wuff-plugin. Then we iterate all subprojects and apply either 'eclipse-bundle' plugin or 'eclipse-rcp-app'.

4. Open console in the directory containing "build.gradle" and "settings.gradle", enter:

  ```bash
  gradle build
  ```

  **Check**: upon successful build there is directory "MyRcpApp/build/output" containing RCP product, specific to our current platform. The product could be started via launch script (.bat or .sh, depending on current platform).