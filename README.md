primogenitor
===

[![Build Status](https://travis-ci.org/io7m/primogenitor.svg)](https://travis-ci.org/io7m/primogenitor)
[![Maven Central](https://maven-badges.herokuapp.com/maven-central/com.io7m.primogenitor/com.io7m.primogenitor/badge.png)](https://maven-badges.herokuapp.com/maven-central/com.io7m.primogenitor/com.io7m.primogenitor)

See https://io7m.github.io/primogenitor/ for more information.

![primogenitor](./src/site/resources/primogenitor.jpg?raw=true)

Note: To build this project, you must use:

```
$ mvn -Denforcer.skip=true clean package
```

The reason for this is that this POM file is intended to be the
root POM for [io7m](http://io7m.com) projects and uses the [Maven
Enforcer](https://maven.apache.org/enforcer/maven-enforcer-plugin/)
plugin to require that descendant projects define values for certain
properties that this root POM leaves empty. Because there is no way
in Maven to have a plugin applied only to descendants, the root POM
actually cannot pass its own checks! Using the `enforcer.skip` property
allows the root POM to be installed and deployed to repositories.

