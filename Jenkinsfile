pipeline {
  agent any
  
  stages {
    stage('Checkout') {
      steps {
        git branch: 'main', url: 'https://github.com/radhwen-chandra/project.git'
      }
    }
    
    stage('Unit Tests') {
      steps {
        dir('tpAchatProject') {
          sh 'mvn test'
        }
      }
    }

    stage('Build') {
      steps {
        dir('tpAchatProject') {
          sh 'mvn clean package'
        }
      }
    }
    
    stage('SonarQube Analysis') {
      steps {
        withSonarQubeEnv('sonar') {
          dir('tpAchatProject') {
            sh 'mvn clean package sonar:sonar'
          }
        }
      }
    }
    
    stage('Quality Gate Status') {
      steps {
        timeout(time: 1, unit: 'HOURS') {
          waitForQualityGate abortPipeline: false
        }
      }
    }
    
    stage('Build Docker Image') {
      steps {
        dir('tpAchatProject') {
          sh 'docker build -t spring .'
        }
      }
    }
    
    stage('Push Docker Image') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'd3427c3c-dc64-4d8e-b4aa-59440db6f55e', usernameVariable: 'saf', passwordVariable: '1234')]) {
          script {
            sh 'docker login -u radhwen7 -p Radhwen1234'
            sh 'docker tag spring radhwen7/spring:latest'
            sh 'docker push radhwen7/spring:latest'
          }
        }
      }
    }
  }
}


  
