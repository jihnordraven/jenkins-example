def app

pipeline {
    agent any

    stages {
        stage("Start Jenkins") {
            steps {
                echo "Start Jenkins Pipeline"
            }
        }
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
        stage("Build docker image") {
            steps {
                echo "Start building docker image"
                script {
                    sh "docker build -t jihnordraven/simple-test:latest ."
                }
                echo "Finish buildiing docker image"
            }
        }
        stage("Finish Jenkins") {
            steps {
                echo "Finish Jenkins Pipeline"
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