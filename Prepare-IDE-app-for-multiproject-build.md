We already [configured IDE products](Configure-IDE-products). Now we prepare IDE app for multiproject build.

1. Create "build.gradle" in "tutorials" folder (parent of "MyIdeApp" folder) 

2. Move "buildscript" and "repositories" from "tutorials/MyIdeApp/build.gradle" to "tutorials/build.gradle", so that two scripts look like this:

  "tutorials/build.gradle":
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

  subprojects {
    repositories {
      mavenLocal()
      jcenter()
    }
  }
  ```

  "tutorials/MyIdeApp/build.gradle":
  ```groovy
  apply plugin: 'java'
  apply plugin: 'eclipse-ide-app'
    
  products {
    product platform: 'linux', arch: 'x86_32'
    product platform: 'linux', arch: 'x86_64'
    product platform: 'windows', arch: 'x86_32'
    product platform: 'windows', arch: 'x86_64'
    archiveProducts = true
  }
  ```

3. Create "settings.gradle" in "tutorials" folder (parent of "MyIdeApp" folder), insert code:

  ```groovy
  include 'MyIdeApp'
  ```

4. Invoke on command line in "tutorials" folder:

  ```shell
  gradle build
  ```

  **CHECK**: Build task generates products in "tutorials/MyIdeApp/build/output" folder.

The example code for this page: [tutorialExamples/IdeApp-3](../tree/master/tutorialExamples/IdeApp-3).

Next page: [Create Eclipse bundle and use it in IDE app](Create-Eclipse-bundle-and-use-it-in-IDE-app).