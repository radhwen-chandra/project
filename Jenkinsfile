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
        sh 'mvn clean package -DskipTests'
      }
    }
    
    stage('Unit Tests') {
      steps {
        sh 'mvn test'
      }
    }
    
    stage('Code Quality') {
      steps {
        sh 'mvn sonar:sonar -Dsonar.projectKey=votre-projet-key -Dsonar.host.url=votre-sonar-url'
      }
    }
    
    stage('Deploy to Nexus') {
      steps {
        sh 'mvn deploy -DskipTests'
      }
    }
    
    stage('Build Docker Image') {
      steps {
        sh 'docker build -t nom-image-docker .'
      }
    }
    
    stage('Push to DockerHub') {
      steps {
        withCredentials([usernamePassword(credentialsId: 'votre-credential-id', usernameVariable: 'DOCKERHUB_USERNAME', passwordVariable: 'DOCKERHUB_PASSWORD')]) {
          sh 'docker login -u radhwen7 -p radhwen1234'
          sh 'docker push spring1'
        }
      }
    }
    
    stage('Run with Docker Compose') {
      steps {
        sh 'docker-compose up -d'
      }
    }
    
    stage('Test Angular Services') {
      steps {
        // Effectuer les tests avec les interfaces de la partie Angular
      }
    }
  }
}
