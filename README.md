# attlasian-jgit-flow
Sample project that demostrates the functionality and use of `jgitflow` plugin provided by attlasian here - https://bitbucket.org/atlassian/jgit-flow/wiki/Home

Its a maven plugin that produces gitflow style releases.

## Gitflow 
GitFlow is one of the popular branching strategy in the software development practice. It mostly focuses on what kind of branches to set up and how to merge them together. This process helps in desgining better pipeline workflow to speed up the controlled S/W release processes.

## Release Process
![GitFlow](https://user-images.githubusercontent.com/38158144/68937127-dd3bfc80-07c1-11ea-9631-bd365e47aa2a.png)

1. Your mainstream branch where continuous development will happen is, `development`.
2. Feature branches will be checked out from `development` and pull request for them will be raised against development.
3. `release` branch is cut from development. (Any bug-fixed that was missed during development branch testing will be done in this branch.
4. Finally, upon QA sign-off on release branch, you will merge `release` branch into master and as well as back to `development`

Here comes the jgit flow plugin that is aligned with gitflow process with extra bit of automation by handling the version and pom updates automatically.

## Walkthrough (README still in progess .......)

