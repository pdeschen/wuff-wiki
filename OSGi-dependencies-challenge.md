OSGi has it's own dependency mechanisms, unrelated to gradle or maven. This is probably OK from conceptual point of view, but can seriously challenge our capability of managing middle-size to big-size projects. Typically we have to resolve the following questions:
- How are we going to program project/component dependencies? Should we duplicate everything - first define dependencies in OSGi manifests, then in gradle/maven configuration? Or should we use some dependency translation mechanism?
- OSGi does not have concept of transitive dependencies, so how we avoid duplicating dependencies across projects?
- If we use non-OSGi libraries, should we wrap them as OSGi bundles? Or is it better to include them privately into each client OSGi bundle?
- How to automate multiproject setup assembly with our favourite build tool (gradle), if many dependencies are OSGi?

Eclipse IDE addresses some of these issues, but not all. For example, there are still no transitive dependencies, no buld-tool integration and no easy way to wrap non-OSGi libraries. The mechanism of features was an attempt to compensate for lack of transitive dependencies, but in fact it turned out to be another layer of complexity. 

Eclipse Tycho is already an improvement, since it provides build-tool integration and dependency translation. Still, we think there should be a better way to manage and build our projects - with less configuration and more flexibility.

