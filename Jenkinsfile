pipeline {
  agent any

  environment {
    COMPOSE_PROJECT_NAME = 'recipeapp'
  }

  stages {
    stage('Checkout') {
      steps {
        git 'https://github.com/KowsikaJ/CICD.git' // Replace with your repository URL
      }
    }

    stage('Build Docker Images') {
      steps {
        echo 'Building Docker images...'
        sh 'docker-compose build'
      }
    }

    stage('Run Containers') {
      steps {
        echo 'Stopping old containers...'
        sh 'docker-compose down || true'  // Use || true to avoid errors if no containers are running

        echo 'Starting new containers...'
        sh 'docker-compose up -d'
      }
    }

    // Optional Test Stage (if you have any tests)
    stage('Run Tests') {
      steps {
        echo 'Running tests...'
        sh 'npm test' // Or replace with the appropriate test command
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
