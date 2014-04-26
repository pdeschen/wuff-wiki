We already know how to [program plugin.xml for eclipse-bundle](plugin.xml-for-eclipse-bundle). Now we will program "plugin.xml" for eclipse-equinox-app.

### Compile and inspect default "plugin.xml"

Take [equinox application](../tree/master/tutorialExamples/EquinoxApp-1) that we created in [Equinox tutorial](Create-first-Equinox-app) as a starting point.

Invoke on command line: `gradle build`.

Open file "tutorials/MyEquinoxApp/build/libs/MyEquinoxApp-1.0.0.0.jar", it contains "plugin.xml" with the following content:

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
- id="Application": can be any string, was assigned to class name.
- class="myequinoxapp.Application": must be a qualified class name.

### Customize application extension-point

Let's customize extension-point "org.eclipse.core.runtime.applications". Our motivation could be that we want different application id. Create folder "tutorials/MyEquinoxApp/src/main/resources", create file "plugin.xml" in it, insert content:

```xml
<plugin>
  <extension id="myappid" point="org.eclipse.core.runtime.applications">
    <application>
      <run class="myequinoxapp.Application"/>
    </application>
  </extension>
</plugin>
```

### Compile and inspect custom application extension-point

Invoke on command line: `gradle build`.

Open file "tutorials/MyEquinoxApp/build/libs/MyEquinoxApp-1.0.0.0.jar", open "plugin.xml" - now it contains our application extension-point, not the default one.

---

The example code for this page: [tutorialExamples/PluginXml-3](../tree/master/tutorialExamples/PluginXml-3).

Next page: [plugin.xml for eclipse-rcp-app](Plugin.xml-for-eclipse-rcp-app).