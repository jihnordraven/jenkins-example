def app

pipeline {
    agent any

    stages {
        stage("Check SCM") {
            steps {
                echo "Start checking scm"
                checkout scm
                echo "Finish checking scm"
            }
        }
        stage("Unit test") {
            steps {
                echo "Start unit testing"
                script {
                    sh "npm install"
                    sh "npm run test"
                }
                echo "Finish unit testing"
            }
        }
        stage("E2E test") {
            steps {
                echo "Start e2e testing"
                script {
                    sh "npm run test:e2e"
                }
                echo "Finish e2e testing"
            }
        }
        stage("Build docker image") {
            steps {
                echo "Start building docker image"
                script {
                    app = docker.build("jihnordraven/simple-test")
                }
                echo "Finish buildiing docker image"
            }
        }
        stage("Finish") {
            steps {
                echo "Finish successfully"
            }
        }
        // stage("Push docker image") {
        //     steps {
        //         echo "Start pushing docker image"
        //         script {
        //             docker.withRegistry("https://registry.hub.docker.com", "jihnordraven") {
        //                 app.push("${env.BUILD_ID}_${env.ENV_TYPE}_${env.GIT_COMMIT}")
        //             }
        //         }
        //     }
        // }
        // stage("Delete docker image") {
        //     steps {
        //         script {
        //             sh "docker rmi -f jihnordraven/simple-test"
        //         }
        //     }
        // }
    }
}