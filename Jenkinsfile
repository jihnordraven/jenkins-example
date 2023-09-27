def app

pipeline {
    agent any

    environment {
        ENV_TYPE  = "production"
        PORT      = 3094
        NAMESPACE = "freedomindz-site"
        PROJECT   = "simple-test"
        REGISTERY = "registry.hub.docker.com"
        
        IMAGE_NAME        = "${env.BUILD_ID}_${env.ENV_TYPE}_${env.GIT_COMMIT}"
        DEPLOYMENT_NAME   = "simple-test"
        DOCKER_BUILD_NAME = "${env.REGISTRY_HOSTNAME}/${env.PROJECT}:${env.IMAGE_NAME}"
        REGISTRY_HOSTNAME = "jihnordraven"
    }

    stages {
        stage("SCM Chekout") {
            steps {
                echo "SCM checkout start..."
                checkout scm
                echo "Finished checkout SCM"
            }
        }
        stage("Unit test") {
            steps {
                echo "Start unit test"
                    script {
                        sh "npm install"
                        sh "npm run test"
                    }
                echo "End unit test"
            }
        }
        stage("e2e test") {
            steps {
                echo "Start e2e test"
                    script {
                        sh "npm run test:323"
                    }
                echo "End e2e test"
            }
        }
        stage("Build docker image") {
            steps {
                echo "Start build docker image"
                    script {
                        app = docker.build("${env.DOCKER_BUILD_NAME}", "--build-arg service=${env.SERVICE} --build-arg port=${env.PORT} -f ./apps/${env.SERVICE}/Dockerfile ./")
                    }
                echo "End build docker image"
            }
        }
        stage('Push docker image') {
            steps {
                echo "Push image started..."
                    script {
                        docker.withRegistry("https://${env.REGISTRY}", 'freedomindz-site') {
                            app.push("${env.IMAGE_NAME}")
                        }
                     }
                echo "Push image finished..."
            }
        }
        stage("Delete image local") {
            steps {
                script {
                    sh "docker rmi -f ${env.DOCKER_BUILD_NAME}"
                }
            }
        }
        stage("Deploy to kubernetes") {
            steps {
                withKubeConfig([credentialsId: 'prod-kubernetes']) {
                    sh "kubectl apply -f deployment.yaml"
                    sh "kubectl rollout status deployment/${env.DEPLOYMENT_NAME} --namespace=${env.NAMESPACE}"
                    sh "kubectl get services -o wide"
                }
            }
        }
    }
}