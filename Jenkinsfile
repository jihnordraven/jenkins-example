pipeline {
    agent any

    stages {
        stage("Start") {
            steps {
                echo "Start Jenkins CI/CD"
            }
        }
        stage("Checkout SCM") {
            steps {
                echo "Start checking scm"
                checkout scm
                echo "Finish checking scm"
            }
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
                    withCredentials([string(credentialsId: 'dockerhubpwd', variable: 'dockerhubpwd')]) {
                        sh "docker login -u flyingmerch123 -p ${dockerhubpwd}"
                    }
                    sh "docker push flyingmerch123/simple-test:latest"
                }
                echo "Finish pushing docker image"
            }
        }
        stage("Delete local image") {
            steps {
                echo "Start deleting docker image"
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