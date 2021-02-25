
pipeline {
  agent any
    
  tools {nodejs "node"}
    
  stages {
        
    //stage('Cloning Git') {
    //  steps {
    //    git 'https://github.com/danieldeles/nodejs-demoapp.git'
    //    
    //  }
    //}

    stage('Checkout'){
      steps {
        checkout scm
      }
    }
        
    stage('Install dependencies') {
      steps {
        sh 'cd src && npm install'
      }
    }



    stage('Run Tests') {
      parallel { 


        stage('Test') {
          steps {
            sh 'cd src && npm test'
          }
        } 

        stage('Test Shell1') {
          steps {
            sh 'date && echo TestShell1'
            sh 'echo Test Shell1_1 && sleep 25 && echo Test Shell1_2'
            sh 'date && echo TestShell1'
          }
        } 

            stage('Test Shell2') {
          steps {
            sh 'date && echo TestShell1'
            sh 'echo Test Shell2_1 && sleep 15 && echo Test Shell2_2'
            sh 'date && echo TestShell1'
          }
        }
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
