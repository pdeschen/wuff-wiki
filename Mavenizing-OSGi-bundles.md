What "mavenizing" means?

When OSGi-bundle is being "mavenized", the following happens:

    The program generates pom.xml for every OSGi-bundle (of eclipse distribution, for example). The generated pom.xml contains maven coordinates "group:artifact:version", where "group" is constant (could be "eclipse", for example), "artifact" corresponds to OSGi-bundle name, "version" corresponds to OSGi-bundle version.

    The program compares every required-bundle of the given OSGi-bundle against other mavenized OSGi-bundles and, when match found, converts it to maven dependency.

    The program automatically finds language-fragments of the given OSGi-bundle and adds them as optional maven dependencies.

    When the program has access to source OSGi-bundles (from eclipse-SDK, for example), it automatically adds them as source-jars to their master mavenized OSGi-bundles.

    The program publishes mavenized OSGi-bundles to maven repository, either local ($HOME/.m2/repository) or remote. Of course, you are in control of which repository is used for publishing.

As the result, you get complete and consistent representation of OSGi-bundles as a set of maven artifacts with dependencies. Combined with maven or gradle, it can greatly simplify building OSGi/eclipse applications.