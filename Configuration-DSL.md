:construction: 

This part is yet under construction!

---

We can fully configure Wuff via "wuff" project extension. This extension is automatically created for us, as soon as we use one of Wuff plugins. The extension supports the following DSL:

```groovy
wuff {
  localMavenRepositoryDir = new File(System.getProperty('user.home'), '.m2/repository')

  wuffDir = new File(System.getProperty('user.home'), '.wuff')

  selectedEclipseVersion = '4.3.2'

  eclipseVersion('4.3.2') {
  }
}
```