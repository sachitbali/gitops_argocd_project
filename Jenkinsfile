pipeline {
    agent any
    environment {
        DOCKERHUB_USERNAME = "sachitbali"
        APP_NAME = "gitops-argocd_CI"
        IMAGE_TAG = "${BUILD_NUMBER}"
        IMAGE_NAME = "${DOCKERHUB_USERNAME}/${APP_NAME}".toLowerCase() // Convert to lowercase
        REGISTRY_CREDS = 'dockerhub'
    }
    
    stages {
        stage('Check Out SCM') {
            steps {
                script {
                    def branchName = params.BRANCH_NAME ?: 'main'
                    git branch: branchName, url: 'https://github.com/sachitbali/gitops_argocd_project.git'
                }
            }
        }
        
        stage('Build Docker Image') {
            steps {
                script {
                    docker_image = docker.build "${IMAGE_NAME}:${IMAGE_TAG}"
                }
            }
        }
        stage('Push docker image'){
            steps{
                script{
                    docker.withRegistry('',REGISTRY_CREDS){
                        docker_image.push("$BUILD_NUMBER")
                        docker_image.push('latest')
                    }
                }
            }
        }
        stage('Docker remove the image'){
            steps{
                script{
                    "docker rmi ${IMAGE_NAME}:${IMAGE_TAG}"
                    "docker rmi ${IMAGE_NAME}:latest"
                }
            }
        }
    }
    
    }
