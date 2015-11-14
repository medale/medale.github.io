---
layout: post
title: "Maven - Local Dependencies"
description: "Download all dependencies to a local repository/offline"
category: "maven"
tags: ["maven","build"]
---

# Useful Maven Commands for offline dependencies

## Show the actual pom settings

    mvn help:effective-pom

## Dependency plugin to manage dependencies

    mvn dependency:tree
    mvn dependency:analyze

### Download dependencies (with sources and javadocs) to local repo

    mvn dependency:go-offline dependency:sources -Dmaven.repo.local=/tmp/repo
    mvn dependency:go-offline dependency:sources -Dclassifier=javadoc -Dmaven.repo.local=/tmp/repo


## Create a local repo with all dependencies

    mvn clean install -Dmaven.repo.local=/tmp/repo

    or add the following to settings.xml default profile:
    <properties>
       <downloadSources>true</downloadSources>
       <downloadJavadocs>true</downloadJavadocs>
    </properties>

    mvn dependency:go-offline dependency:sources -Dmaven.repo.local=/tmp/repo
    mvn dependency:go-offline dependency:sources -Dclassifier=javadoc -Dmaven.repo.local=/tmp/repo

## Offline build

    mvn -o install
