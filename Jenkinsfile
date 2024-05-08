pipeline {
    agent any
    tools {
	    nodejs "node"
	    sonarqube 'sonarqube'
	}
    
    stages {

        stage('Fetch code'){
            steps {
                git branch: 'dev', url: 'https://github.com/harshall-devops/online-exam-portal.git'
            }
        }

        stage('Test'){
            steps {
                sh 'mvn test'
            }
        }

        stage ('CODE ANALYSIS WITH CHECKSTYLE'){
            steps {
                sh 'mvn checkstyle:checkstyle'
            }
            post {
                success {
                    echo 'Generated Analysis Result'
                }
            }
        }

        stage('SonarQube analysis') {
            steps {
                script {
                    def scannerHome = tool 'sonar4.7'
                    withSonarQubeEnv('sonar') {
                        sh '''${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=Exam-portal \
                           -Dsonar.projectName=Exam-Portal \
                           -Dsonar.projectVersion=1.0 \
                           -Dsonar.sources=src/ \
                           -Dsonar.java.binaries=target/test-classes/com/visualpathit/account/controllerTest/ \
                           -Dsonar.junit.reportsPath=target/surefire-reports/ \
                           -Dsonar.jacoco.reportsPath=target/jacoco.exec \
                           -Dsonar.java.checkstyle.reportPaths=target/checkstyle-result.xml'''
                    }
                }
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
