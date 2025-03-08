pipeline {
    agent { label 'Slave01' }

    environment {
        DOCKER_CREDENTIALS = credentials('DockerHub')
    }

    stages {
        stage('Build Backend Image') {
            steps {
                dir('backend') {
                    sh 'docker build -t mohamedessam1911/manager-backend:latest .'
                }
            }
        }

        stage('Build Frontend Image') {
            steps {
                dir('frontend') {
                    sh 'docker build -t mohamedessam1911/manager-frontend:latest .'
                }
            }
        }

        stage('Docker Login') {
            steps {
                sh 'echo $DOCKER_CREDENTIALS_PSW | docker login -u $DOCKER_CREDENTIALS_USR --password-stdin'
            }
        }

        stage('Push Images') {
            steps {
                sh 'docker push mohamedessam1911/manager-backend:latest'
                sh 'docker push mohamedessam1911/manager-frontend:latest'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                sh 'kubectl apply -f k8s/'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
