
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

    stage('Building image') {
      steps{
        script {
          dockerImage = docker.build imagename
        }
      }
    }

    stage('Build image') {
      steps {
        script {
          /* This builds the actual image; synonymous to
          * docker build on the command line */

          docker = docker.build("getintodevops/hellonode")
        } 
      } 
    }  
    
    /*
     stage('Test image') {
        steps {
          script {
            // Ideally, we would run a test framework against our image.
            // For this example, we're using a Volkswagen-type approach ;-) 

            docker.inside {
                sh 'cd src && npm test'
                }
            }
        }
    }
    */
    



    stage('Run Tests') {
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


        stage('Tests Postman-newman') {
          steps {
            sh 'cd src && /usr/local/bin/newman run ./tests/postman_collection.json --suppress-exit-code 1'
          }
        } 

        ///usr/local/bin/docker

        //stage('Building image 0') {
        //  steps {
        //      sh 'docker build --label v1.0.0 -t myrepo/myapp:v1.0.0'
        //  }
        //}


      }
    } 

/*
    stage('Building image2') {
      steps{
        script {
          dockerImage = docker.build imagename
        }
      }
    }

*/


    
  }
}
