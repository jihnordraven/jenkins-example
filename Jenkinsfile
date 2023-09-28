pipeline {
    agent any

    stages {
        stage("Hello") {
            steps {
                echo "Hello World"
            }
        }
        stage("Build docker image") {
            steps {
                echo "Start building docker image"
                script {
                    docker.build('jihnordraven/jenkins-example:latest')
                    // sh "docker build -t jihnordraven/jenkins-example:latest ."
                }
                echo "Finish building docker image"
            }
        }
    }
}