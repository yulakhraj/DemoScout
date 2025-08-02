pipeline {
    agent {
        label 'windows'  // Make sure your Jenkins agent has this label and Docker + Trivy installed
    }

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

        stage('Scan with Trivy') {
            steps {
                bat """
                    echo Scanning Docker image with Trivy...
                    trivy image --exit-code 0 --severity MEDIUM,HIGH,CRITICAL %IMAGE_NAME% || exit 0
                """
            }
        }

        stage('Post-Scan Actions') {
            steps {
                echo '✅ Vulnerability scan complete. Check the console output above.'
            }
        }
    }
}
