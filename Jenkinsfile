pipeline {
  agent any
  
  stages {
    stage('Checkout') {
      steps {
        git 'https://github.com/radhwen-chandra/project.git'
      }
    }
    
    stage('Build') {
      steps {
        sh 'mvn clean package'
      }
    }
    
    stage('Unit Tests') {
      steps {
        sh 'mvn test'
      }
    }
    
    
    stage('Build Docker Image') {
      steps {
        sh 'docker build -t spring1 .'
      }
    }
  }
}
