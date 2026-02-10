pipeline {
    agent any

    environment {
        IMAGE_NAME = "travel-space-image"
        CONTAINER_NAME = "travel-space"
        PORT = "8081"
    }

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/SusmithaVarma11/Spaceship.git',
                    credentialsId: 'Susmitha_Varma'
            }
        }

        stage('Stop Old Container') {
            steps {
                bat '''
                docker ps -aq --filter "name=%CONTAINER_NAME%" | findstr . && docker stop %CONTAINER_NAME% && docker rm %CONTAINER_NAME%
                '''
            }
        }

        stage('Build Docker Image') {
            steps {
                bat '''
                docker build -t %IMAGE_NAME% .
                '''
            }
        }

        stage('Run Docker Container') {
            steps {
                bat '''
                docker run -d ^
                 --name %CONTAINER_NAME% ^
                 -p %PORT%:80 ^
                 %IMAGE_NAME%
                '''
            }
        }
    }

    post {
        success {
            echo "✅ Travel Space deployed successfully on port ${PORT}"
        }
        failure {
            echo "❌ Pipeline failed"
        }
    }
}
