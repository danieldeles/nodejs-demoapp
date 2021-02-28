/*
The Official Documentation (Portuguese) is in: 
https://github.com/danieldeles/nodejs-demoapp/blob/master/Docs/Doc_KK_Pipeline.pdf
*/

pipeline {


  agent any
    
  tools {nodejs "node"}
    
  stages {
        

    stage('Clone repository'){
      steps {
        // Checkout GitHub repository
        checkout scm

      }
    }
        

    stage('Install dependencies') {
      steps {
        // Install NodeJS dependencies
        sh 'cd src && npm install'

      }
    }




    stage('Run Tests in Parallel') {
      
      // Run tests in parallel
      parallel { 

        // Code analysis in SonarQube
        stage('Tests Quality Check SonarQube') {
          steps {
           sh "/home/ddd/developer/sonar-scanner-4.6.0.2311-linux/bin/sonar-scanner \
                -Dsonar.projectKey=delesderrier_nodejs-kk \
                -Dsonar.sources=src \
                -Dsonar.host.url=http://10.0.0.100:9000 \
                -Dsonar.login=8a4b975a864dbb3d6d3ea663a8d479b7f21b4cc6"
          }
        }

        // Mocha Tests
        stage('Tests Mocha') {
          steps {
            sh 'cd src && npm test'
          }
        } 

        // Postman tests
        stage('Tests Postman-Newman') {
          steps {
            sh 'cd src && /usr/local/bin/newman run ./tests/postman_collection.json --suppress-exit-code 1'
          }
        } 


      }
    } 



    // Deploy Docker image using Dockerfile
    stage('Build image') {
      steps {
        script {

          docker = docker.build("delesderrier/nodejs-kk")
          
        } 
      } 
    }  
    

    // Push new image to DockerHub
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
