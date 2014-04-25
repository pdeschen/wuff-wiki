Wuff generates default "plugin.xml" for the following applied plugins: "eclipse-bundle", "eclipse-equinox-app", "eclipse-ide-app", "eclipse-rcp-app".

If we provide our own "plugin.xml" (either in "src/main/resources" or project root), Wuff merges our version and generated version to produce the resulting "plugin.xml".

The purpose of default "plugin.xml" is to eliminate/minimize manual coding of extension points for views, perspectives, applications and products. For example, if eclipse plugin contains java class XyzView.java, Wuff generates 