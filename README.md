primogenitor
===

[![Build Status](https://img.shields.io/travis/io7m/primogenitor.svg?style=flat-square)](https://travis-ci.org/io7m/primogenitor)
[![Maven Central](https://img.shields.io/maven-central/v/com.io7m.primogenitor/com.io7m.primogenitor.svg?style=flat-square)](http://search.maven.org/#search%7Cga%7C1%7Cg%3A%22com.io7m.primogenitor%22)
[![Maven Central (snapshot)](https://img.shields.io/nexus/s/https/oss.sonatype.org/com.io7m.primogenitor/com.io7m.primogenitor.svg?style=flat-square)](https://oss.sonatype.org/content/repositories/snapshots/com/io7m/primogenitor/)

The [io7m](http://io7m.com) root [POM](https://maven.apache.org/pom.html).

![primogenitor](./src/site/resources/primogenitor.jpg?raw=true)

## Building

To build this project, you must use:

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

## Features

The `primogenitor` POM builds on existing Maven conventions and enforces stricter conventions of its own. The POM is heavily commented and exposes several configurable properties. See the `properties` section in the POM for details.

By setting the parent of a project's POM file to `com.io7m.primogenitor`, the project receives the following services:

* Enforcement of the presence of POM properties required for Maven Central: Descendant POMs are required to provide `description`, `url`, and `name` elements.
* Enforcement of a minimum Java version (currently `9`) with a friendly error message if the project is built on a JDK that is too old.
* Enforcement of a minimum Maven version (currently `3.5.0`) with a friendly error message if the project is built with a version of Maven that is too old.
* The immediate rejection of circular dependencies.
* Enforcement of reproducible builds: No (transitive) dependency may depend on a `SNAPSHOT` version.
* Enforcement of plugin versioning: No plugin may be added without an explicit version number.
* Insertion of [Git](http://www.git-scm.com) commit identifiers into the produced Jar file `Implementation-Build` manifest field with the [buildnumber-maven-plugin](http://www.mojohaus.org/buildnumber-maven-plugin/). This assists with tracing exactly which artifacts were used to produce an application.
* Byte-for-byte reproducible Jar files with the [reproducible-build-maven-plugin](http://zlika.github.io/reproducible-build-maven-plugin/index.html).
* Automatic insertion of [OSGi](http://www.osgi.org) metadata into the produced Jar files using the [bnd-maven-plugin](https://github.com/bndtools/bnd/tree/master/maven/bnd-maven-plugin). Sensible default values are chosen based on metadata given in the POM file, and this can be overridden on a per-module basis.
* Automatic checking of [semantic versioning](https://semver.org/) using the [bnd-baseline-maven-plugin](https://github.com/bndtools/bnd/tree/master/maven/bnd-baseline-maven-plugin). Bytecode is analyzed and the build fails if, for example, binary incompatible changes have been made without incrementing the project's major version number.
* Automatic source style checks using [Checkstyle](https://maven.apache.org/plugins/maven-checkstyle-plugin/). Rules are consulted from external Maven artifacts in order to facilitate sharing rules across large numbers of projects and enforcing a consistent style everywhere.
* Automated bug-checking with [SpotBugs](https://spotbugs.github.io/spotbugs-maven-plugin/index.html). The build fails if probable bugs are found.
* Automatic production of JavaDoc and `-sources` Jar files, sufficient for publishing to Maven Central.
* Automatic signing of artifacts with the [maven-gpg-plugin](https://maven.apache.org/plugins/maven-gpg-plugin/), sufficient for publishing to Maven Central.
* Incorporation of the [nexus-staging-maven-plugin](https://github.com/sonatype/nexus-maven-plugins/tree/master/staging/maven-plugin) for publishing releases to Maven Central with a single `mvn clean deploy` command.
* Analysis of dependency issues (unused dependencies, undeclared but used transient dependencies) with the [maven-dependency-plugin](https://maven.apache.org/plugins/maven-dependency-plugin/). The build fails if any dependency issues are discovered.
* Generation of minimalist single page sites with [minisite](https://io7m.github.io/minisite/).
* Automatic collection of code coverage information with [JaCoCo](http://www.jacoco.org/).
* All plugin versions are specified with Maven properties, and can therefore be overridden in the (unfortunate) case of a plugin being buggy, and can be efficiently updated with the [versions-maven-plugin](http://www.mojohaus.org/versions-maven-plugin/).
* The ability to turn off all optional features and produce a build as quickly as possible by setting the property `io7m.quick_build` to `true` on the command line: `$ mvn -Dio7m.quick_build=true clean package`.

