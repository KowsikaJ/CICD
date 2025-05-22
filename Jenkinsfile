pipeline {
  agent any

  environment {
    DOCKER_COMPOSE_FILE = 'docker-compose.yml'
  }

  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Build Docker Images') {
      steps {
        echo '🔧 Building Docker images (no cache)...'
        sh 'docker-compose build --no-cache'
      }
    }

    stage('Stop Old Containers') {
      steps {
        echo '🛑 Stopping old containers...'
        sh 'docker-compose down --remove-orphans'
      }
    }

    stage('Deploy New Containers') {
      steps {
        echo '🚀 Starting new containers...'
        sh 'docker-compose up -d'
      }
    }

    stage('Verify Backend Logs') {
      steps {
        echo '📄 Backend container logs:'
        sh 'docker logs recipeapp-backend-1 || true'
      }
    }
  }

  post {
    success {
      echo '✅ Application successfully deployed!'
    }
    failure {
      echo '❌ Deployment failed.'
    }
  }
}
