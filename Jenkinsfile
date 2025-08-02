pipeline {
    agent any

    environment {
        IMAGE_NAME = 'nginx:latest'
    }

    stages {
        stage('Pull Docker Image') {
            steps {
                bat "docker pull %IMAGE_NAME%"
            }
        }

        stage('Docker Scout Scan') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker-hub-creds', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                    bat """
                        echo Logging in to Docker Hub...
                        docker login -u %DOCKER_USER% -p %DOCKER_PASS%
                        docker scout quickview %IMAGE_NAME%
                    """
                }
            }
        }

        stage('Post-Scan Actions') {
            steps {
                echo '✅ Docker Scout analysis complete.'
            }
        }
    }
}

