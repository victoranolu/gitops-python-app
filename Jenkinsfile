pipeline {
    agent any
    environment {
        DOCKERHUB_USERNAME = "poormanalfred"
        APP_NAME = "gitops-python-app"
        IMAGE_TAG = "${BUILD_NUMBER}"
        IMAGE_NAME = "${DOCKERHUB_USERNAME}" + "/" + "${APP_NAME}"
        REGISTRY_CREDENTIALS = "dockerhub"
    }

    stages {
        stage('Print Build Number'){
            steps {
                sh 'echo $BUILD_NUMBER'
            }
        }
        stage('Cleanup Workspace'){
            steps {
                script {
                    cleanWs()
                }
            }
        }
        stage('Checkout SCM'){
            steps {
                git branch: 'main', 
                credentialsId: 'github', 
                url: 'https://github.com/victoranolu/gitops-python-app.git'
            }
        }
        stage('Build Docker Image'){
            steps {
                script {
                    docker_image = docker.build "${IMAGE_NAME}"
                }
            }
        }
        stage('Push Docker Image'){
            steps {
                script {
                    docker.withRegistry('', REGISTRY_CREDENTIALS ){
                        docker_image.push('$BUILD_NUMBER')
                        docker_image.push('latest')
                    }
                }
            }
        }
    }
}



        // stage('Build Docker with Dockerfile'){
        //     steps {
        //         sh "docker build -t ${IMAGE_NAME}:${IMAGE_TAG} ."
        //         sh "docker build -t ${IMAGE_NAME}:latest ."
        //     }
        // }
        // stage('Push to Docker Hub'){
        //     steps {
        //         withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'pass', usernameVariable: 'user')]) {
        //             sh "docker login -u $user --password $pass"    
        //         }
        //     }
        // }