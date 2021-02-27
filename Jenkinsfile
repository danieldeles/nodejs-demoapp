
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




    stage('Run Tests in Parallel') {
      parallel { 


        stage('Tests Quality Check SonarQube') {
          steps {
           sh "/home/ddd/developer/sonar-scanner-4.6.0.2311-linux/bin/sonar-scanner \
                -Dsonar.projectKey=nodejs-demoapp \
                -Dsonar.sources=src \
                -Dsonar.host.url=http://10.0.0.100:9000 \
                -Dsonar.login=8a4b975a864dbb3d6d3ea663a8d479b7f21b4cc6"
          }
        }


        stage('Tests Mocha') {
          steps {
            sh 'cd src && npm test'
            //npm run test-junit
          }
        } 


        stage('Tests Postman-Newman') {
          steps {
            sh 'cd src && /usr/local/bin/newman run ./tests/postman_collection.json --suppress-exit-code 1'
          }
        } 


      }
    } 




    stage('Build image') {
      steps {
        script {

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
