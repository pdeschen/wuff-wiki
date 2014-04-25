We already programmed [manifest attributes in MANIFEST.MF](Manifest-attributes-in-MANIFEST.MF). Now we will learn how to do expression injection in MANIFEST.MF.

1. The easiest way to do expression injection in MANIFEST.MF is to use gradle capabilities. Add new instruction to jar/manifest in "build.gradle":

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