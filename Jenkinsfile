pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'sufiyaannn84/java-ci-cd-app'
        DOCKERHUB_CREDENTIALS_ID = 'dockerhub-creds' // Replace with your Jenkins DockerHub credentials ID
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/sufiyaannn84/java-CI-CD-Pipeline.git'
            }
        }

        stage('Build with Maven') {
            steps {
                sh 'mvn clean install'
            }
        }

        stage('Run Tests') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build("${DOCKER_IMAGE}:${BUILD_NUMBER}")
                }
            }
        }

        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('', "${DOCKERHUB_CREDENTIALS_ID}") {
                        dockerImage.push()
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deployment step goes here (Docker run, Kubernetes, etc)'
            }
        }
    }

    post {
        success {
            echo "Pipeline completed successfully ✅"
        }
        failure {
            echo "Pipeline failed ❌"
        }
    }
}
