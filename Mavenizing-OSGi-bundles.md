What "mavenizing" means? When Wuff mavenizes OSGi-bundles, the following happens:

1. Wuff generates pom.xml for every OSGi-bundle (of eclipse distribution, for example). The generated pom.xml contains maven coordinates "group:artifact:version", where "group" is constant (could be "eclipse", for example), "artifact" corresponds to OSGi-bundle name, "version" corresponds to OSGi-bundle version.

2. Wuff compares every required-bundle of the given OSGi-bundle against other mavenized OSGi-bundles and, when match found, converts it to maven dependency.

3. Wuff automatically finds language-fragments of the given OSGi-bundle and adds them as optional maven dependencies.

4. When Wuff configuration specifies source OSGi-bundles (of eclipse-SDK, for example), Wuff automatically adds them as source-jars to their master mavenized OSGi-bundles.

5. Wuff publishes mavenized OSGi-bundles to maven repository, either local ($HOME/.m2/repository) or remote. Of course, you are in control of which repository is used for publishing.

As the result, you get complete and consistent representation of OSGi-bundles as a set of maven artifacts with dependencies.