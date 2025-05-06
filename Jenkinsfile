pipeline {
    agent any

    environment {
        DOCKERHUB_CREDENTIALS = credentials('dockerhub')
        FRONTEND_IMAGE = 'yourdockerhub/chefclaude-frontend'
        BACKEND_IMAGE  = 'yourdockerhub/chefclaude-backend'
    }

    stages {
        stage('Clone') {
            steps {
                git 'https://github.com/KowsikaJ/CICD.git'
            }
        }

        stage('Build Docker Images') {
            steps {
                script {
                    docker.build("${FRONTEND_IMAGE}", "./frontend")
                    docker.build("${BACKEND_IMAGE}", "./backend")
                }
            }
        }

        stage('Push Images') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', DOCKERHUB_CREDENTIALS) {
                        docker.image("${FRONTEND_IMAGE}").push()
                        docker.image("${BACKEND_IMAGE}").push()
                    }
                }
            }
        }

        stage('Deploy Containers') {
            steps {
                sh 'docker-compose down || true'
                sh 'docker-compose up -d'
            }
        }
    }
}
