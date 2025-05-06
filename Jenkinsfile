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
        sh 'docker-compose build'
      }
    }

    stage('Run Containers') {
      steps {
        sh 'docker-compose down' // stop old containers if any
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
