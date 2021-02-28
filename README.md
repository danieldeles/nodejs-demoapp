# Pipeline KK

The **Official Documentation** (in Portuguese) is: https://github.com/danieldeles/nodejs-demoapp/blob/master/Docs/Doc_KK_Pipeline.pdf

There are also two **videos** inside the **Docs** folder. They show the pipeline working on Jenkins Labs.

## Objective:

This document describes **how to develop a pipeline for the CI** (Continuous Integration) process using the GitHub project.

This project code using NodeJS was forked: https://github.com/benc-uk/nodejs-demoapp

Pipeline prerequisites:

- Have a code analysis step using SonarQube
- Have a unit testing validation step
- Have tests in parallel
- Generate image in Docker
- Push the versioned image to a public repository
- Do not use GitHub Actions


In addition, some characteristics deserve to be highlighted because they influence decisions and tools:

- Source code in Node.js - the Express framework with EJS templates was used.
- It has some ready tests:
  - Mocha tests at: src / tests /
  - Postman tests at: src / package.json
- Dockerfile at the root of the project.


# Pipeline Structure Summary

Based on the pre-defined conditions, a pipeline workflow was created:

- Project checkout on GitHub
- Install as NodeJS dependencies
- Run tests in parallel:
  - Code analysis in SonarQube
  - Mocha Tests
  - Postman tests
- Generate image in Docker using Dockerfile
- Push the versioned image to DockerHub

----------
