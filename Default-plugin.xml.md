Wuff generates default "plugin.xml" for the following applied plugins: "eclipse-bundle", "eclipse-equinox-app", "eclipse-ide-app", "eclipse-rcp-app".

Whenever we supply our own "plugin.xml" (either in "src/main/resources" or project root), Wuff merges our version and generated version to produce resulting "plugin.xml".