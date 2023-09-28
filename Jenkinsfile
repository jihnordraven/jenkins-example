pipeline {
    agent any

    stages {
        stage("Unit test") {
            echo "Start unit test"
            steps {
                // sh "npm install"
                // sh "npm run test"
            }
            echo "Finish unit test"
        }
        stage("E2e test") {
            echo "Start e2e test"
            script {
                // sh "npm run test:e2e"
            }
            echo "Finish e2e test"
        }
        stage("Build docker image") {
            steps {
                echo "Start building docker image"
                script {
                    sh "docker build -t flyingmerch123/simple-test:latest ."
                }
                echo "Finish building docker image"
            }
        }
        stage("Push docker image") {
            steps {
                echo "Start pushing docker image"
                script {
                    withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerhubpwd')]) {
                        sh "docker login -u flyingmerch13 -p ${dockerhubpwd}"
                    }
                    sh "docker push flyingmerch123/simple-test:latest"
                }
                echo "Finish pushing docker image"
            }
        }
        stage("Delete local image") {
            steps {
                echo "Start deleting docker image"
                script {
                    sh "docker rmi -f flyingmerch123/simple-test:latest"
                }
                echo "Finish deleting docker image"
            }
        }
        stage("Finish") {
            steps {
                echo "Finish Jenkins CI/CD successfully"
            }
        }
    }
}