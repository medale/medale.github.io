---
layout: post
title: "Scala Build Tooling"
description: "Scala build tools - bloop and coursier"
category: "scala"
tags: ["programming", "scala", "build"]
---

# Faster Scala Builds with bloop and coursier

One common complaint about Scala is the long time lag for compiles, running
tests and starting up Scala programs. Another challenge about dependency management
in general is the use of libraries depending on other libraries etc. that
all must be downloaded.

Enter the Scala Center's [bloop build server](https://scalacenter.github.io/bloop/)
to reduce compile, test and run times and the [coursier sbt plugin](https://github.com/coursier/sbt-coursier)
to parallelize library dependency downloads with an all Scala dependency management
tool.

## Bloop server

The Bloop server as supports the [build server protocol (bsp)](https://github.com/scalacenter/bsp) that allows
integration with the IntelliJ Idea IDE and integrates with sbt, Maven, Gradle and Mill.

### Ubuntu Install

```
# Installs to $HOME/.bloop
curl -L https://github.com/scalacenter/bloop/releases/download/v1.3.2/install.py | python

# Add bloop to PATH in .bashrc
PATH=$HOME/.bloop:....

# Add autocompletion ~/.bash_profile
. $HOME/.bloop/bash/bloop
```

### Start/Stop via systemd

```
systemctl --user enable $HOME/.bloop/systemd/bloop.service
systemctl --user daemon-reload
journalctl --user-unit bloop
systemctl --user status bloop
systemctl --user start bloop # also stop/restart
```

### sbt integration
```
# ${PROJECT_ROOT}/project/plugins.sbt
# https://scalacenter.github.io/bloop/setup
addSbtPlugin("ch.epfl.scala" % "sbt-bloop" % "1.3.2")

sbt
> bloopInstall #re-run when changing dependencies or build-related artifacts, modules etc.

Now compile, test run on bloop server
```

## Coursier sbt plugin

```
# Edit or create ${PROJECT_ROOT}/project/project/plugins.sbt
// https://github.com/coursier/sbt-coursier/releases
// Setup: https://get-coursier.io/docs/sbt-coursier
// also see project/plugins.sbt
addSbtPlugin("io.get-coursier" % "sbt-coursier" % "2.0.0-RC3-1")

# Edit or create ${PROJECT_ROOT}/project/plugins.sbt
// https://github.com/coursier/sbt-coursier/releases
// Setup: https://get-coursier.io/docs/sbt-coursier
// also see project/project/plugins.sbt
addSbtCoursier
classpathTypes += "maven-plugin"
coursierUseSbtCredentials := true
```

### Checksum problems
When using the 1.x version of the coursier sbt plugin I ran into some problems
with a 3rd party artifact checksum not being correct. Following the
[comments on coursier ticket 319](https://github.com/coursier/coursier/issues/319)
I added the following but haven't needed it since in other projects:

```
coursierChecksums := Nil
coursierArtifactsChecksums := Nil
```
