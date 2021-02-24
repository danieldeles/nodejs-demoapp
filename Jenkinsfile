
pipeline {
  agent any
    
  tools {nodejs "node"}
    
  stages {
        
    stage('Cloning Git') {
      steps {
        git 'https://github.com/danieldeles/nodejs-demoapp.git'
        
      }
    }
        
    stage('Install dependencies') {
      steps {
        sh 'cd src && npm install'
      }
    }
     
    stage('Test') {
      steps {
         sh 'cd src && npm test'
      }
    } 
    

    stage('SonarQube Analysis') {
      steps {
        sh "/home/jenkins/tools/hudson.plugins.sonar.SonarRunnerInstallation/sonarqubescanner/bin/sonar-scanner -Dsonar.host.url=http://localhost:9000 -Dsonar.projectName=meanstackapp -Dsonar.projectVersion=1.0 -Dsonar.projectKey=meanstack:app -Dsonar.sources=. -Dsonar.projectBaseDir=/Users/danielsilva/.jenkins/workspace/sonarqube_pipeline"
      }
    }
    
  }
}
