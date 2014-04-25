We already know how to [program plugin.xml for eclipse-bundle](plugin.xml-for-eclipse-bundle). Now we will program "plugin.xml" for eclipse-equinox-app.

Take [equinox application](../tree/master/tutorialExamples/EquinoxApp-1) that we created in [Equinox tutorial](Create-first-Equinox-app) as a starting point.

1. Invoke on command line: `gradle build`, then open file "tutorials/MyEquinoxApp/build/libs/MyEquinoxApp-1.0.0.0.jar", it contains "plugin.xml" with the following content:

  ```xml
  <plugin>
    <extension id="Application" point="org.eclipse.core.runtime.applications">
      <application>
        <run class="myequinoxapp.Application"/>
      </application>
    </extension>
  </plugin>
  ```

  We see that Wuff recognized file "tutorials/MyEquinoxApp/src/main/java/myequinoxapp/Application.java" as an application and that it automatically inserted extension-point for it. In general, Wuff recognizes any files matching to patterns `'**/Application.groovy', '**/Application.java'` as application files and inserts extension-point "org.eclipse.core.runtime.applications" for each of them (although normally there's only one application per eclipse-equinox-app).

  Explanation of attributes:
  - id="Application": assigned to class name.
  - class="myequinoxapp.Application": assigned to qualified class name.
