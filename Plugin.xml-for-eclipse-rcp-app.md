We already know how to [program plugin.xml for eclipse-equinox-app](plugin.xml-for-eclipse-equinox-app). Now we will program "plugin.xml" for eclipse-rcp-app.

### Compile and inspect default "plugin.xml"

Take [rcp application](../tree/master/tutorialExamples/RcpApp-1) that we created in [RCP tutorial](Create-first-RCP-app) as a starting point.

Invoke on command line: `gradle build`.

Open file "tutorials/MyRcpApp/build/libs/MyRcpApp-1.0.0.0.jar", it contains "plugin.xml" with the following content:

```xml
<plugin>
  <extension id="Application" point="org.eclipse.core.runtime.applications">
    <application>
      <run class="myrcpapp.Application"/>
    </application>
  </extension>
  <extension id="product" point="org.eclipse.core.runtime.products">
    <product application="MyRcpApp.Application" name="MyRcpApp"/>
  </extension>
  <extension point="org.eclipse.ui.perspectives">
    <perspective id="MyRcpApp.Perspective" name="MyRcpApp Perspective" class="myrcpapp.Perspective"/>
  </extension>
  <extension point="org.eclipse.ui.views">
    <view id="MyRcpApp.View" name="MyRcpApp View" class="myrcpapp.View"/>
  </extension>
  <extension point="org.eclipse.ui.perspectiveExtensions">
    <perspectiveExtension targetID="MyRcpApp.Perspective">
      <view id="MyRcpApp.View" standalone="true" minimized="false" relative="org.eclipse.ui.editorss" relationship="left"/>
    </perspectiveExtension>
  </extension>
</plugin>
```

Extension-point "org.eclipse.core.runtime.applications" is the same as in [plugin.xml for eclipse-equinox-app](Plugin.xml-for-eclipse-equinox-app).

Extension-points "org.eclipse.ui.perspectives", "org.eclipse.ui.views" and "org.eclipse.ui.perspectiveExtensions" are the same as in [plugin.xml for eclipse bundle](plugin.xml-for-eclipse-bundle).

There is new generated extension-point: "org.eclipse.core.runtime.products". As we see, it was automatically linked to extension-point "org.eclipse.core.runtime.applications" via "product/@application" attribute.

### Customize application extension-point

Create folder "tutorials/MyRcpApp/src/main/resources", create file "plugin.xml" in it, insert content:

```xml
<plugin>
  <extension id="myappid" point="org.eclipse.core.runtime.applications">
    <application>
      <run class="myrcpapp.Application"/>
    </application>
  </extension>
</plugin>
```

### Compile and inspect custom application extension-point

Invoke on command line: `gradle build`.

Open file "tutorials/MyRcpApp/build/libs/MyRcpApp-1.0.0.0.jar", open "plugin.xml". Now extension-points "org.eclipse.core.runtime.applications" and "org.eclipse.core.runtime.products" look a bit different:

```xml
<plugin>
  <extension id="myappid" point="org.eclipse.core.runtime.applications">
    <application>
      <run class="myrcpapp.Application"/>
    </application>
  </extension>
  <extension id="product" point="org.eclipse.core.runtime.products">
    <product application="MyRcpApp.myappid" name="MyRcpApp"/>
  </extension>
  <extension point="org.eclipse.ui.perspectives">
    <perspective id="MyRcpApp.Perspective" name="MyRcpApp Perspective" class="myrcpapp.Perspective"/>
  </extension>
  <extension point="org.eclipse.ui.views">
    <view id="MyRcpApp.View" name="MyRcpApp View" class="myrcpapp.View"/>
  </extension>
  <extension point="org.eclipse.ui.perspectiveExtensions">
    <perspectiveExtension targetID="MyRcpApp.Perspective">
      <view id="MyRcpApp.View" standalone="true" minimized="false" relative="org.eclipse.ui.editorss" relationship="left"/>
    </perspectiveExtension>
  </extension>
</plugin>
```

As we see, Wuff does not generate extension-point "org.eclipse.core.runtime.applications", it uses the one provided by us. Also it links the generated extension-point "org.eclipse.core.runtime.products" to it.

### Customize product extension-point

Edit file "tutorials/MyRcpApp/src/main/resources/plugin.xml", insert content:

```xml
  <extension id="myproductid" point="org.eclipse.core.runtime.products">
    <product application="MyRcpApp.myappid" name="Very nice app">
      <property name="windowImages" value="icons/icon_16x16.png,icons/icon_32x32.png,icons/icon_64x64.png,icons/icon_128x128.png"/>
      <property name="aboutText" value="This program has big future!"/>
      <property name="aboutImage" value="images/logo.png"/>
      <property name="startupForegroundColor" value="FFFFFF"/>
      <property name="startupMessageRect" value="28,218,421,20"/>
      <property name="startupProgressRect" value="28,243,421,15"/>
    </product>
  </extension>  
```