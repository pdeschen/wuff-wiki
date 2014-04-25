We already programmed [manifest attributes in MANIFEST.MF](Manifest-attributes-in-MANIFEST.MF). Now we will learn how to do manifest expression injection.

1. The easiest way to do manifest expression injection is to use gradle/groovy capabilities. Edit file "tutorials/MyOsgiPlugin/build.gradle", insert code to jar/manifest:

  ```groovy
  instruction 'Project-Info', "${project.name} compiled on ${new Date()}"
  ```

2. Invoke on command line:

  ```
  gradle build
  ```

3. Open file "tutorials/MyOsgiPlugin/build/libs/MyOsgiPlugin-1.0.0.0.jar", open "META-INF/MANIFEST.MF", it should contain:

  ```
  Project-Info: MyOsgiPlugin compiled on Fri Apr 25 12:46:22 CEST 2014
  ```

4. We can also program expression injection in MANIFEST.MF. Edit the file "tutorials/MyOsgiPlugin/src/main/resources/META-INF/MANIFEST.MF", insert code:

  ```
  Project-Description: ${project.description}
  ```

5. Edit file "tutorials/MyOsgiPlugin/build.gradle", insert code:

  ```groovy
  description = 'this is example project'
  wuff {
    filterManifest = true
  }
  ```

6. Invoke on command line:

  ```
  gradle build
  ```

7. Open file "tutorials/MyOsgiPlugin/build/libs/MyOsgiPlugin-1.0.0.0.jar", open "META-INF/MANIFEST.MF", it should contain:

  ```
  Project-Description: this is example project
  ```
