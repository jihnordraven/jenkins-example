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
        // stage("Push docker image") {
        //     steps {
        //         echo "Start pushing docker image"
        //         script {
        //             sh "docker push jihnordraven/simple-test:latest"
        //         }
        //         echo "Finish pushing docker image"
        //     }
        // }
        // stage("Deploy to kubernetes") {
        //     steps {
        //         echo "Start deploying to kubernetes"
        //         script {
        //             sh "kubectl apply -f deployment.yaml"
        //             sh "kubectl apply -f loadBalancer.yaml"
        //         }
        //         echo "Finish deploying to kubernetes"
        //     }
        // }
        // stage("Delete docker image localy") {
        //     steps {
        //         echo "Start deleting docker image localy"
        //         script {
        //             sh "Deletedocker rmi jihnordraven/simple-test:latest"
        //         }
        //         echo "Finish deleting docker image localy"
        //     }
        // }
    }
}
// comment