Each time Wuff processes an OSGi-bundle[1], it generates an OSGi manifest. As input for manifest generation, it uses various project properties: version, name, dependencies, classpath etc. The generated manifest does not pollute program sources: it is generated as a temporary file in "build" folder. Wuff instructs gradle Jar task to include the generated OSGi manifest into JAR-file.

When the programmer gives no additional instructions on OSGi-manifest generation, the generated OSGi manifest is called **default manifest**.

Lets inspect how default manifest looks like.

1. Create folder "tutorials/MyOsgiManifest", create file "build.gradle" in it, insert code:

  ```groovy
  buildscript {
    repositories {
      mavenLocal()
      jcenter()
    }

    dependencies {
      classpath 'org.akhikhl.wuff:wuff-plugin:0.0.1'
    }
  }

  apply plugin: 'java'
  apply plugin: 'osgi-bundle'

  repositories {
    mavenLocal()
    jcenter()
  }
  ```

[1]: In Wuff context OSGi-bundle is a gradle project with one of the plugins applied: "eclipse-bundle", "eclipse-equinox-app", "eclipse-ide-app", "eclipse-ide-bundle", "eclipse-rcp-app", "osgi-bundle".