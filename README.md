# Pipeline KK

The **Official Documentation** (Portuguese) is in: https://github.com/danieldeles/nodejs-demoapp/blob/master/Docs/Doc_KK_Pipeline.pdf

There are also two **videos** inside the **Docs** folder. They show the pipeline working on Jenkins Labs.

## Objective:

This project describes **how to develop a pipeline for the CI** (Continuous Integration) process using:
- GitHub 
- Jenkins
- SonarQube
- Mocha
- Docker
- DockerHub

This project was forked: https://github.com/benc-uk/nodejs-demoapp

Pipeline prerequisites:

- Code analysis using SonarQube
- Unit tests
- Tests in parallel
- Buid image in Docker
- Push the image to a public repository
- Can't use GitHub Actions


# Pipeline Structure Summary

Based on the pre-defined conditions, a pipeline workflow was created:

- Checkout the Project on GitHub
- Install NodeJS dependencies
- Run tests in parallel:
  - Code analysis in SonarQube
  - Mocha Tests
  - Postman tests
- Deploy Docker image using Dockerfile
- Push new image to DockerHub

