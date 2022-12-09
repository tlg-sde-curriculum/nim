---
title: Overview
nav_order: 1
---

{% include abbreviations.md %}
{% assign javadocs = site.aux_links.Javadocs %}

# {{ page.title }}
{:.no_toc}

<details markdown="block">
  <summary>Contents</summary>
* TOC
{:toc}
</details>

## Introduction

In this project, you'll develop---with your instructor's guidance---a text-mode implementation of _Nim,_ a simple mathematical game. In doing this, you'll exercise and strengthn your knowledge and skill with the Java language, the Java standard library, OOP concepts & practices, and key software engineering principles.

## Assumptions

To complete this assignment, you must have the following software installed; however, note that under certain conditions (described in the footnotes), specific version of the JDKs or Gradle will be downloaded automatically,

* JDK 11[^jdk-version]
* Git 2.0 or higher
* Gradle 6.0 or higher (Gradle v7.6 is used in the build.[^gradle-version])
* IDE suitable for Java development.

[^jdk-version]: If Gradle does not detect a suitable JDK installed, it will provision the build by downloading the required JDK, following the rules given in ["Toolchains for JVM projects: Precedence](https://docs.gradle.org/current/userguide/toolchains.html#sec:precedence){:target='_blank'}. The downloaded JDK will be available to subsequent Gradle builds.

[^gradle-version]: The Gradle project in the code repository for this project includes the [_Gradle Wrapper_](https://docs.gradle.org/current/userguide/gradle_wrapper.html). As long as builds are performed using the Gradle Wrapper (done by default in IntelliJ IDEA and some other IDEs, and via a configurable option in virtually all others), the required version of Gradle will be downloaded if it's not already present on the local system; after downloading, it will remain available for subsequent Gradle builds. 

## [Project & repository](project-repository/)

For your implementation, you won't be creating a new project or repository from scratch; instead, you'll be creating a repository from a template; that repository will be located in your GitHub account, and you'll clone it to your local system. 

As you progress in the implementation, you should commit to Git frequently and push to GitHub on a regular basis. 
