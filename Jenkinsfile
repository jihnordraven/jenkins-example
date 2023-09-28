pipeline {
    agent any

    stages {
        stage("Start") {
            steps {
                echo "Start Jenkins"
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
                    sh "docker build -t jihnordraven/simple-test:latest ."
                }
                echo "Finish building docker image"
            }
        }
    }
}
// comment