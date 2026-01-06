pipeline {
    agent any

    stages {

        stage('Build Images') {
            steps {
                sh 'docker compose build'
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

                    docker tag devops-capstone-backend:latest $DOCKER_USER/devops-backend:latest
                    docker tag devops-capstone-frontend:latest $DOCKER_USER/devops-frontend:latest

                    docker push $DOCKER_USER/devops-backend:latest
                    docker push $DOCKER_USER/devops-frontend:latest
                    '''
                }
            }
        }

        stage('Deploy (CD)') {
            steps {
                sh '''
                docker compose -f docker-compose.deploy.yml down || true
                docker compose -f docker-compose.deploy.yml pull
                docker compose -f docker-compose.deploy.yml up -d
                '''
            }
        }

        stage('Health Check') {
            steps {
                sh 'sleep 10'
                sh 'curl http://localhost:5000/health'
            }
        }
    }
}
