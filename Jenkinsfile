pipeline {
    agent any
    tools {
	    nodejs "node"
         maven "MAVEN3"
	    jdk "OracleJDK11"
	    
	}

    environment {
            CI = 'true'
npm_config_prefix = '/home/ubuntu/.npm-global'
        }
    
    stages {

        stage('Fetch code'){
            steps {
                git branch: 'dev', url: 'https://github.com/harshall-devops/online-exam-portal.git'
            }
        }
        


       

       
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
