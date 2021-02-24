
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
  }
}
