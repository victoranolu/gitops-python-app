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
    }
}