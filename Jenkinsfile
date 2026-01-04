pipeline {
    agent any

    stages {
        stage('Build Docker Images') {
            steps {
                sh 'docker compose -f docker-compose.yml build'
            }
        }
        stage('Push Images to Docker Hub') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'dockerhub-creds',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    sh '''
                    docker login -u $DOCKER_USER -p $DOCKER_PASS

                    docker tag devops-capstone-pipeline-backend:latest $DOCKER_USER/devops-backend:latest
                    docker tag devops-capstone-pipeline-frontend:latest $DOCKER_USER/devops-frontend:latest

                    docker push $DOCKER_USER/devops-backend:latest
                    docker push $DOCKER_USER/devops-frontend:latest
                    '''
                }
            }
        }

        

        stage('Run Containers') {
            steps {
                sh 'docker compose -f docker-compose.yml up -d'
            }
        }

        stage('Health Check') {
            steps {
                sh 'sleep 10'
                sh 'curl http://localhost:5000/health'
            }
        }
    }

    post {
        always {
            sh 'docker compose -f docker-compose.yml down'
        }
    }
}
