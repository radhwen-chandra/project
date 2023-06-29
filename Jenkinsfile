pipeline {
  agent any
  
  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', url: 'https://github.com/radhwen-chandra/project.git'
      }
    }
    
    stage('Build') {
      steps {
         dir('spring') {
          sh 'mvn clean package'
       }
     }
    }
    stage('Unit Tests') {
      steps {
         dir('spring') {
          sh 'mvn test'
       }
     }
    }
    
    
    stage('Build Docker Image') {
      steps {
        sh 'docker build -t spring1 .'
      }
    }
  }
}
