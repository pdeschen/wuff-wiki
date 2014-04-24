Each time Wuff processes an OSGi-bundle[1] it generates an OSGi manifest. As input for manifest generation, it uses various project properties: version, name, dependencies, classpath etc. The generated manifest does not pollute program sources: it is placed to "build/osgi" folder. Wuff instructs gradle Jar task to include the generated OSGi manifest into JAR-file.

When the programmer gives no additional instructions on OSGi-manifest generation, the generated OSGi manifest is called **default manifest**.

[1]: In Wuff context OSGi-bundle is a gradle project with one of the plugins applied: "eclipse-bundle", "eclipse-equinox-app", "eclipse-ide-app", "eclipse-ide-bundle", "eclipse-rcp-app", "osgi-bundle".