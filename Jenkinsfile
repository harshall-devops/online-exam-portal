pipeline {
    agent any
    
    stages {
        stage('Build Backend Image') {
            steps {
                script {
                    docker.build('backend-app:1.0', './backend')
                }
            }
        }
        
        stage('Build Frontend Image') {
            steps {
                script {
                    docker.build('frontend-app:1.0', './frontend')
                }
            }
        }

        stage('Build User Frontend Image') {
            steps {
                script {
                    docker.build('user-frontend-app:1.0', './user-portal-frontend')
                }
            }
        }
    }
}
