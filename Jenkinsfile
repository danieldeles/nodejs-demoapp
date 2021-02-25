
pipeline {

  environment {
    imagename = "yenigul/hacicenkins"
    registryCredential = 'yenigul-dockerhub'
    dockerImage = ''
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

        stage('Test Shell1') {
          steps {
            sh 'date && echo TestShell1'
            sh 'echo Test Shell1_1 && sleep 25 && echo Test Shell1_2'
            sh 'date && echo TestShell1'
          }
        } 

        stage('Test') {
          steps {
            sh 'cd src && npm test'
          }
        } 


      }
    } 
    

    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build imagename
        }
      }
    }

    stage('Deploy Image') {
      steps{
        script {
          docker.withRegistry( '', registryCredential ) {
            dockerImage.push("$BUILD_NUMBER")
             dockerImage.push('latest')

          }
        }
      }
    }

    
  }
}
