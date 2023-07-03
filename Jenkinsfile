pipeline {
  agent any
  
  stages {
    stage('Checkout') {
      steps {
        git branch: 'master', url: 'https://github.com/radhwen-chandra/project.git'
      }
    }
    
    stage('Build') {
      steps {
        dir('tpAchatProject') {
          sh 'mvn clean package'
        }
      }
    }
    
    stage('Unit Tests') {
      steps {
        dir('tpAchatProject') {
          sh 'mvn test'
        }
      }
    }
    
    stage('Build Docker Image') {
      steps {
        sh 'docker build -t spring7 .'
      }
    }
  }
}
