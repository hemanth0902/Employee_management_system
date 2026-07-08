pipeline {
    agent any

    environment {
        BACKEND_IMAGE = "hemanthpoojary/employee-backend:v3"
        FRONTEND_IMAGE = "hemanthpoojary/employee-frontend:v3"
    }

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build Backend') {
            steps {
                dir('ems-backend') {
                    sh 'mvn clean package -DskipTests'
                }
            }
        }

        stage('Build Frontend') {
            steps {
                dir('ems-frontend') {
                    sh 'npm install'
                    sh 'npm run build'
                }
            }
        }

        stage('Docker Build Backend') {
            steps {
                dir('ems-backend') {
                    sh 'docker build -t $BACKEND_IMAGE .'
                }
            }
        }

        stage('Docker Build Frontend') {
            steps {
                dir('ems-frontend') {
                    sh 'docker build -t $FRONTEND_IMAGE .'
                }
            }
        }

        stage('Docker Push Backend') {
            steps {
                sh 'docker push $BACKEND_IMAGE'
            }
        }

        stage('Docker Push Frontend') {
            steps {
                sh 'docker push $FRONTEND_IMAGE'
            }
        }

        stage('Deploy') {
            steps {
                echo 'Deployment stage'
            }
        }
    }
}
