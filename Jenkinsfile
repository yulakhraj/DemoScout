pipeline {
    agent any

    environment {
        IMAGE_NAME = 'nginx:latest'
    }

    stages {
        stage('Pull Docker Image') {
            steps {
                bat """
                    echo Pulling nginx image...
                    docker pull %IMAGE_NAME%
                """
            }
        }

        stage('Docker Scout Scan') {
            steps {
                bat """
                    echo Running Docker Scout image analysis...
                    docker scout quickview %IMAGE_NAME%
                """
            }
        }

        stage('Post-Scan Actions') {
            steps {
                echo '✅ Docker Scout analysis complete. Review the findings above.'
            }
        }
    }
}
