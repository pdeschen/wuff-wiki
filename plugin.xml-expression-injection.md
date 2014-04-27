We already programmed ["plugin.xml" for IDE app](Plugin.xml-for-eclipse-ide-app). Now we can how to do "plugin.xml" expression injection.

Let's take an [example Eclipse plugin](../tree/master/tutorialExamples/PluginXml-1) we created in ["plugin.xml" for Eclipse bundle](plugin.xml-for-eclipse-bundle).

Edit the file "tutorials/MyEclipsePlugin/src/main/resources/plugin.xml", change content to:

```xml
<plugin>
  <extension point="org.eclipse.ui.views">
    <view id="myviewid" name="${project.ext.myViewName}" class="myeclipseplugin.MyView"/>
  </extension>
</plugin>
```

Edit the file "tutorials/MyEclipsePlugin/build.gradle", insert code:

```groovy
wuff {
  filterPluginXml = true
}

ext {
  myViewName = 'test123'
}
```

Invoke on command line: `gradle build`.

Open file "tutorials/MyBuildPlugin/build/libs/MyBuildPlugin-1.0.0.0.jar", open "plugin.xml", it should contain:

```xml
<plugin>
  <extension point="org.eclipse.ui.views">
    <view id="myviewid" name="test123" class="myeclipseplugin.MyView"/>
  </extension>
</plugin>
```

Note that expressions in "plugin.xml" are **not** expanded by default. We must set wuff.filterPluginXml=true to enable this feature.

Note that sometimes dollar sign, **$**, is used for Eclipse-specific expressions in "plugin.xml". Typical example is localized location of intro pages: 

```xml
<extension point="org.eclipse.ui.intro.config">
  <config id="MyRcpApp.introConfigId" introId="MyRcpApp.intro" content="$nl$/intro/introContent.xml">
    <presentation home-page-id="homePageId" standby-page-id="homePageId">
      <implementation kind="html"/>
    </presentation>
  </config>
</extension>
```

Expression injection would produce errors with such Eclipse-specific expressions, because dollar sign has special meaning to it (see more information at [Groovy templates documentation](http://groovy.codehaus.org/Groovy+Templates)). To avoid the errors, we need to escape dollar sign:

```xml
<extension point="org.eclipse.ui.intro.config">
  <config id="MyRcpApp.introConfigId" introId="MyRcpApp.intro" content="\$nl\$/intro/introContent.xml">
    <presentation home-page-id="homePageId" standby-page-id="homePageId">
      <implementation kind="html"/>
    </presentation>
  </config>
</extension>
```
