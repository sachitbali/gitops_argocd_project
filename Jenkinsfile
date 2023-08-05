pipeline{
    agent any
    environment{
        DOCKERHUB_USERNAME = "sachitbali"
        APP_NAME = "gitops-argocd_CI"
        IMAGE_TAG = "${BUILD_NUMBER}"
        IMAGE_NAME = "${DOCKERHUB_USERNAME}" + "/" + "${APP_NAME}"
        REGISTERY_CREDS = 'dockerhub'
    }

    stages  {
        stage('check out scm'){
            steps{
                script{
                    git branch: 'main', url: 'https://github.com/sachitbali/gitops_argocd_project.git'
                }
            }
        }
        }
        
    }
}