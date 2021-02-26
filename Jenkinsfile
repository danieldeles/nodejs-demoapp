
pipeline {

  environment {
    imagename = "yenigul/hacicenkins"
    registryCredential = 'yenigul-dockerhub'
    dockerImage = ''
    varTest = 'xixixixixixi'
  }

  agent any
    
  tools {nodejs "node"}
    
  stages {
        
    //stage('Cloning Git') {
    //  steps {
    //    git 'https://github.com/danieldeles/nodejs-demoapp.git'
    //    
    //  }
    //}

    stage('Clone repository'){
      steps {
        checkout scm
      }
    }
        

    stage('Install dependencies') {
      steps {
        sh 'cd src && npm install'
      }
    }



    stage('Tests Code') {
      parallel { 


        //stage('Code Quality Check via SonarQube') {
        //  steps {
        //   sh "/Users/danielsilva/.jenkins/tools/sonar-scanner-4.6.0.2311-macosx/bin/sonar-scanner \
          //      -Dsonar.projectKey=nodejs-demoapp \
          //      -Dsonar.sources=src \
          //      -Dsonar.host.url=http://10.0.0.49:9000 \
          //     -Dsonar.login=8a4b975a864dbb3d6d3sa663a8d479b7f21b4cc6"
        // }
        //}


        stage('Tests Mocha') {
          steps {
            sh 'cd src && npm test'
            //npm run test-junit
          }
        } 





      }
    } 

            stage('Tests Postman-newman') {
          steps {
            //sh 'cd src && test-postman'
            sh 'cd src && /usr/local/bin/newman run ./tests/postman_collection.json '
          }
        } 
    

    

    
  }
}
