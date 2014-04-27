We already know how to [program "plugin.xml" for Equinox app](plugin.xml-for-eclipse-equinox-app). Now we will program "plugin.xml" for RCP app.

### Compile and inspect default "plugin.xml"

Let's take an [example of RCP app](../tree/master/tutorialExamples/RcpApp-5) that we built in [RCP tutorial](Add-splash-to-RCP-app).

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

### Compile and inspect custom product extension-point

Invoke on command line: `gradle build`.

Open file "tutorials/MyRcpApp/build/libs/MyRcpApp-1.0.0.0.jar", open "plugin.xml", expect to see:

```xml
<plugin>
  <extension id="myappid" point="org.eclipse.core.runtime.applications">
    <application>
      <run class="myrcpapp.Application"/>
    </application>
  </extension>
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

As we see, "plugin.xml" contains our application and product extension points, not the default ones.

### Default intro extension points

Let's take an [example of RCP app with intro page](../tree/master/tutorialExamples/RcpApp-6) that we built in [RCP tutorial](Add-intro-page-to-RCP-app).

Invoke on command line: `gradle build`.

Open file "tutorials/MyRcpApp/build/libs/MyRcpApp-1.0.0.0.jar", it contains "intro/introContent.xml" with the following content:

```xml
<introContent>
  <page id="homePageId" url="welcome.html"/>
</introContent>
```

Wuff generated this file for us, because it have seen, then there is "intro/welcome.html" page, but no "intro/introContent.xml". If we would provide our own version of "intro/introContent.xml" (either in "src/main/resources" or in project's root), Wuff would use just that.

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
  <extension point="org.eclipse.ui.intro">
    <intro id="MyRcpApp.intro" class="org.eclipse.ui.intro.config.CustomizableIntroPart"/>
    <introProductBinding introId="MyRcpApp.intro" productId="MyRcpApp.product"/>
  </extension>
  <extension point="org.eclipse.ui.intro.config">
    <config id="MyRcpApp.introConfigId" introId="MyRcpApp.intro" content="intro/introContent.xml">
      <presentation home-page-id="homePageId" standby-page-id="homePageId">
        <implementation kind="html"/>
      </presentation>
    </config>
  </extension>
</plugin>
```

Wuff generated two new extension points: "org.eclipse.ui.intro" and "org.eclipse.ui.intro.config", which are linking product and "introContent.xml". Similarly to application and product extension points - as soon as we provide our own versions of "org.eclipse.ui.intro" and "org.eclipse.ui.intro.config", Wuff would use these versions, not the automatically generated ones.

---

Next page: ["plugin.xml" for IDE app](Plugin.xml-for-eclipse-ide-app)