
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

    stage('Test Shell1') {
      steps {
         sh 'echo OI1 && sleep 5 && echo OI2'
      }
    } 

        stage('Test Shell2') {
      steps {
         sh 'echo OI1 && sleep 15 && echo OI2'
      }
    } 
    
    //stage('Test2') {
    //  steps {
    //     sh 'cd src && mocha tests'
    //  }
    //} 

    //stage('SonarQube Analysis') {
    //  steps {
     //   sh "/Users/danielsilva/.jenkins/tools/sonar-scanner-4.6.0.2311-macosx/bin/sonar-scanner \
     //       -Dsonar.host.url=http://localhost:9000 \
     //       -Dsonar.projectName=meanstackapp -Dsonar.projectVersion=1.0 -Dsonar.projectKey=meanstack:app -Dsonar.sources=. \
      //      -Dsonar.projectBaseDir=/Users/danielsilva/.jenkins/workspace/sonarqube_pipeline"
     // }
    //}
    
  }
}
