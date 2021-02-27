
pipeline {

  environment {
    imagename = "danieldeles/node01"
    registryCredential = 'userpassdockerhub'
    dockerImage = ''
    varTest = 'xixixixixixi'
  }

  //def app

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






    stage('Run Tests') {
      parallel { 


        stage('Code Quality Check via SonarQube') {
          steps {
           sh "/home/ddd/developer/sonar-scanner-4.6.0.2311-linux/bin/sonar-scanner \
                -Dsonar.projectKey=nodejs-demoapp \
                -Dsonar.sources=src \
                -Dsonar.host.url=http://10.0.0.100:9000 \
                -Dsonar.login=c86e2fa7-2e41-4f8c-a211-1980773bf8be"
          }
        }


        stage('Tests Mocha') {
          steps {
            sh 'cd src && npm test'
            //npm run test-junit
          }
        } 


        stage('Tests Postman-newman') {
          steps {
            sh 'cd src && /usr/local/bin/newman run ./tests/postman_collection.json --suppress-exit-code 1'
          }
        } 


      }
    } 




    stage('Build image') {
      steps {
        script {
          /* This builds the actual image; synonymous to
          * docker build on the command line */

          docker = docker.build("delesderrier/nodejs-kk")
          
        } 
      } 
    }  
    


    stage('Push image') {
      steps {
        script {

          withCredentials([usernamePassword(credentialsId: 'userpassdockerhub', passwordVariable: 'dockerHubPassword', usernameVariable: 'dockerHubUser')]) {
            sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPassword}"
            sh 'docker push delesderrier/nodejs-kk:latest'
          }

        }
      }
    }


    
  }
}
