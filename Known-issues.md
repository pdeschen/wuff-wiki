### RCP app may hang on Linux with Cinnamon

Eclipse-RCP app may sporadically hang on start, when running on Linux with Cinnamon Desktop. The exact reason for this is unkown, although the following is observed:
- The issue is not specific to Wuff - same behavior is seen with Eclipse-RCP app generated and run under Eclipse IDE.
- The issue is not specific to particular JDK - same behavior is seen with JDK-7 and JDK-8.
- The issue is not reproducible on other desktops - Linux with [XFCE, Mate], Windows.

The issue is fixed by deleting all folders in "configuration" folder of the RCP app.