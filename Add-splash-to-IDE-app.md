We already [added perspective and view to IDE app](Add-perspective-and-view-to-IDE-app). Now we add splash screen to the IDE app.

### Prepare splash screen

Download or create some bmp-file with bit depth 8 or 24 (not 32). Name it "splash.bmp".

Create folder "tutorials/MyIdeApp/src/main/resources", copy splash file into it.

### Compile

Invoke on command line in "tutorials/MyIdeApp" folder: `gradle build`.

Note that we don't have to configure splash screen in configuration files - Wuff does this for us automatically.

### Run

Run the compiled product from command line. The program shows splash screen while starting:

![IdeApp-6-run-1](images/IdeApp-6-run-1.png)

---

The example code for this page: [examples/IdeApp-6](../tree/master/examples/IdeApp-6).

Next page: [Add intro page to IDE app](Add-intro-page-to-IDE-app).