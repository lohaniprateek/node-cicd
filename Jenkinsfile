pipeline {
  agent any

  environment {
    DOCKER_HOST = "tcp://dind:2375"
    IMAGE_NAME = "my-todolist"
  }

  stages {

    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Install & Test') {
      steps {
        sh '''
          cd app
          npm install
          npm test
        '''
      }
    }

    stage('Build Docker Image') {
      steps {
        sh '''
          cd app
          docker build -t $IMAGE_NAME:latest .
        '''
      }
    }

    stage('Deploy with Docker Compose') {
      steps {
        sh '''
          docker compose -f docker-compose.app.yml down || true
          docker compose -f docker-compose.app.yml up -d
        '''
      }
    }
  }
}
