---
layout: page
title: Linux Command Goodies
tagline: Useful Linux commands
---

# Exploring Hardware Environment

## Determine 32 vs. 64-bit OS
    >file /sbin/init
    /sbin/init: ELF 64-bit LSB shared object, x86-64,...

## Determine Ubuntu Version and Version Name
    >lsb_release -a
    Description:	Ubuntu 13.10
    Release:	13.10
    Codename:	saucy
    > cat /etc/*-release
    DISTRIB_ID=Ubuntu
    DISTRIB_RELEASE=13.10
    DISTRIB_CODENAME=saucy
    DISTRIB_DESCRIPTION="Ubuntu 13.10"
    NAME="Ubuntu"
    VERSION="13.10, Saucy Salamander"
    ...

# Network

## Determine other machines on same local subnet

    >/sbin/ifconfig - shows Bcast address, e.g. 192.168.1.255
    >ping -b 192.168.1.255 - shows other machines on local subnet

# Applications

## Slack

### Reset hung Linux Slack client:

    cd ~/.config/Slack
    rm -Rf SS

## Pandoc
* Font sizes: from [https://texblog.org/2012/08/29/changing-the-font-size-in-latex/](https://texblog.org/2012/08/29/changing-the-font-size-in-latex/)
     * \Huge
     * \huge
     * \LARGE
     * \Large
     * \large
     * \normalsize (default)
     * \small
     * \footnotesize
     * \scriptsize
     * \tiny

```bash
pandoc in.md -o out.pdf
pandoc in.md -o out.html
pandoc in.md -o out.html -s --metadata pagetitle="Out"

# Updated for pandoc 2.4 - making slides
DOCNAME=SparkDataEngineering
pandoc -t beamer --pdf-engine=xelatex ${DOCNAME}.md -o ${DOCNAME}.pdf -V theme:metropolis  -V colortheme:default

# Slides
---
header-includes:
 - \usepackage{fvextra}
 - \DefineVerbatimEnvironment{Highlighting}{Verbatim}{breaklines,commandchars=\\\{\}}
 - \usepackage{fontspec}
 - \usepackage{setspace}
title: Data Engineering with Apache Spark
author: Markus Dale, medale@...
date: May 2019
---

# Apache Spark: Data engineering for larger dataset (Vertical Scaling)

![Beefed-up Server](graphics/VerticalScaling.png){height=80%}

# Cluster Manager - Manage cores, memory, special capabilities

![](graphics/ClusterManagers.png)

# Data Science Mission

\Large
* ID malicious GitHub Pull Requests?

# Anatomy of a Spark Application

![](graphics/SparkApplication.png)
\tiny Source: Apache Spark website

# Hello, Spark World!

\scriptsize
scala (code block with three backticks)
import org.apache.spark.sql.SparkSession
...

```

## Open with default application

    xdg-open steps.html
    xdg-open http://cnn.com
