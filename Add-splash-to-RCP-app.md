Provided that we already [created Eclipse bundle and used it in RCP app](Create-Eclipse-bundle-and-use-it-in-RCP-app), now we can add splash screen to the RCP app.

1. Download or create some bmp-file with bit depth 8 or 24 (not 32). Name it "splash.bmp".

2. Create folder "tutorials/MyRcpApp/src/main/resources", copy splash file into it.

3. Invoke on command line in "tutorials" folder:

```shell
gradle build
```

**CHECK**: When you run the product, it shows splash screen before the main window is fully opened.

Note that you don't have to configure splash screen in "plugin.xml" or "plugin_customization.ini" - wuff does this for you automatically.

The example code corresponding to this page is located in [tutorialExamples/RcpApp-5](../tree/master/tutorialExamples/RcpApp-5).