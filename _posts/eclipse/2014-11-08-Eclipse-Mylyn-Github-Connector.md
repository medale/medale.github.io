---
layout: post
title: "Eclipse Mylyn GitHub Connector"
description: "Connecting Eclipse to GitHub Issues"
category: "eclipse"
tags: ["eclipse","luna","github", "mylyn"]
---
{% include JB/setup %}
# Eclipse Mylyn

The Eclipse Mylyn plugin provides task-centric display/artifact management.
Mylyn tracks what files were touched for a given task and as you switch/activate
tasks Eclipse only shows the artifacts for that tasks. There are
also lots of task management features.

Besides local task management there are a variety of Mylyn connectors that allow tasks
to be stored in task tracking tools such as Jira, Trac or GitHub Issues.
GitHub Issues is a nice task tracking framework associated with a GitHub
project.
 
# Tracking GitHub Issues from Eclipse Mylyn

* From Eclipse: Help - Install New Software
* Select Luna Update site: Luna - http://download.eclipse.org/releases/luna
* Filter: GitHub
* Select Eclipse GitHub integration

# Create GitHub Task Repository
* Window - Show View - Other - Mylyn - Task Repositories
* Right click Tasks folder - Add Task Repository
* Select GitHub Issues
* Server: http://github.com/medale/spark-mail
* Add GitHub user id/password
* Validate Settings

This creates a new Bugs - medale/spark-mail issues task repo

# Working on tasks
* Window - Show View - Other - Mylyn - Task List

This shows issues that were already created on GitHub and allows
you to work with those or create new issues remotely.

