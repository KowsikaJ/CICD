pipeline {
    agent any

    environment {
        DOCKERHUB_REPO = 'kowsikaj'
    }

    stages {
        stage('Clone') {
            steps {
                git 'https://github.com/KowsikaJ/CICD.git'
            }
        }

        stage('Docker Login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    sh 'echo $DOCKER_PASS | docker login -u $DOCKER_USER --password-stdin'
                }
            }
        }

        stage('Build Docker Images') {
            steps {
                sh 'docker build -t $DOCKERHUB_REPO/chefclaude-frontend ./frontend'
                sh 'docker build -t $DOCKERHUB_REPO/chefclaude-backend ./backend'
            }
        }

        stage('Push Images') {
            steps {
                sh 'docker push $DOCKERHUB_REPO/chefclaude-frontend'
                sh 'docker push $DOCKERHUB_REPO/chefclaude-backend'
                sh 'docker logout'
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

