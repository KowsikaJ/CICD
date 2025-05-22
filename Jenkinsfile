pipeline {
  agent any

  environment {
    COMPOSE_PROJECT_NAME = 'recipeapp'
  }

  stages {
    stage('Checkout') {
      steps {
        git 'https://github.com/KowsikaJ/CICD.git'
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
        sh 'docker-compose down --remove-orphans || true'
      }
    }

    stage('Deploy New Containers') {
      steps {
        echo '🚀 Starting new containers...'
        sh 'docker-compose up -d'
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
