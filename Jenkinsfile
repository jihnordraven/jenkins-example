pipeline {
    agent any

    stages {
        stage('Checkout SCM') {
            steps {
                echo "Start checkout scm"
                checkout scm
                echo "Finish checkout scm"
            }
        }
        stage('Unit test') {
            steps {
                echo "Start unit test"
                script {
                    sh "npm install"
                    sh "npm run test"
                }
                echo "Finish unit test"
            }
        }
        stage('E2E test') {
            steps {
                echo "Start e2e test"
                script {
                    sh "npm run test:e2e"
                }
                echo "Finish e2e test"
            }
        }
        stage("Build docker image") {
            steps {
                echo "Start build docker image"
                script {

                }
                echo "Finish build docker image"
            }
        }
    }
}