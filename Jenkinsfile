pipeline {
    agent any

    environment {
        APP_NAME = 'DemoApp'
        APP_VERSION = '1.0'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/VR-Sindhujha/jenkins-q3-q4.git'

                echo 'Source code downloaded from GitHub'
            }
        }

        stage('Build') {
            steps {
                bat 'python -m py_compile app.py'
                echo 'Build completed successfully'
            }
        }

        stage('Deploy') {
            steps {
                input message: "Approve deployment of ${APP_NAME} version ${APP_VERSION}?",
                      ok: 'Release'

                bat 'python app.py'
            }
        }
    }

    post {
        success {
            echo 'Deployment completed successfully!'
        }

        aborted {
            echo 'Deployment was aborted!'
        }

        failure {
            echo 'Pipeline failed!'
        }
    }
}