# attlasian-jgit-flow
Sample project that demostrates the functionality and use of `jgitflow` plugin provided by attlasian here - https://bitbucket.org/atlassian/jgit-flow/wiki/Home

Its a maven plugin that produces gitflow style releases. 

To enable this - we add following into `POM.xml`

```
<plugin>
  <groupId>external.atlassian.jgitflow</groupId>
  <artifactId>jgitflow-maven-plugin</artifactId>
  <version>1.0-m5.1</version>
  <configuration>
    <enableSshAgent>true</enableSshAgent>
    <autoVersionSubmodules>true</autoVersionSubmodules>
    <pushFeatures>true</pushFeatures>
    <pushReleases>true</pushReleases>
    <pushHotfixes>true</pushHotfixes>
    <noDeploy>true</noDeploy>
    <flowInitContext>
      <developBranchName>develop</developBranchName>
        <versionTagPrefix>version-</versionTagPrefix>
    </flowInitContext>
    <enableSshAgent>true</enableSshAgent>
    <scmCommentPrefix>DEVOPS-000 </scmCommentPrefix>
  </configuration>
</plugin>
```
Note:- If you are cloning this repo then you need not to add. Its already a part of this sample project.

## Gitflow 
GitFlow is one of the popular branching strategy in the software development practice. It mostly focuses on what kind of branches to set up and how to merge them together. This process helps in desgining better pipeline workflow to speed up the controlled S/W release processes.

## Release Process
![gitflow-release-process](https://user-images.githubusercontent.com/38158144/68986878-ef617d80-0849-11ea-9590-c4a4a36faccb.jpg)

1. Our mainstream branch where continuous development happens, is `develop`.
2. Feature branch is checked out from `develop` and pull request for it raised against `develop`.
3. `release` branch is cut from `develop` once all the intended features merged into `develop`. (Any bug-fixed that was missed during development branch testing will be done in this `release` branch.
4. Finally, upon QA sign-off `release` branch merges into master and as well as back to `develop`

## Why [maven jgitflow](https://bitbucket.org/atlassian/jgit-flow/wiki/Home) ?
maven jgit flow plugin is aligned with the gitflow process with extra bit of automation by handling the version and pom updates automatically freeing us from manual intervention.

## Prerequisites
* Make sure we have JAVA and MAVEN configured correctly along with their ENV variables. such `JAVA_HOME`, `M2_HOME` and `MAVEN_HOME`.

## Walkthrough - hands-on

* **Clone this repo**
```
$ git clone https://github.com/tprakash17/atlassian-jgit-flow.git
```

After cloning make sure you upload this repository to the repo where you have write access. This is required to make sure plugin has all the necessary permissions to automatically merge the code.


* **Checkout feature branch from development**

Make sure you are on `develop` branch before checking out feature.

```
$ git checkout -b feature/DEVOPS-01
```

Make some changes to the code and raise the pull request against `develop` branch and merge it.


* **Start release**

maven `jgitflow` introduces few maven goals such as following to automate release workflow. 

* [jgitflow:release-start](https://bitbucket.org/atlassian/jgit-flow/wiki/goals/release-start) - Prepares the project for a release. Creates a release branch and updates pom(s) with the release version.
* [jgitflow:release-finish](https://bitbucket.org/atlassian/jgit-flow/wiki/goals/release-finish) - Releases the project. Builds the project, Merges the release branch (as per git-flow), optionally pushes changes and updates pom(s) to new development version.

There are few more goals this plugin provides. [More details](https://bitbucket.org/atlassian/jgit-flow/wiki/goals.wiki#!goals-overview)

```
$ mvn jgitflow:release-start
```
This should create a `release` branch with a tag `release/$TAG`. Check if the branch is created `git branch -a`

* **Finish Release**
```
$ mvn jgitflow:release-finish
```

This should automatically update the release version into master and bump the SNAPSHOT into development pom without us handling it manually. 

