pipeline {
    agent any

    environment {
        HARBOR_REGISTRY = "192.168.1.77"
        HARBOR_PROJECT = "view"
        IMAGE_NAME = "view-app"
        IMAGE_TAG = "latest"
        JD_IMAGE = "${HARBOR_REGISTRY}/${HARBOR_PROJECT}/${IMAGE_NAME}:${IMAGE_TAG}"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Phurich283/test-deploy', credentialsId: 'github_token'
            }
        }
        stage('Build') {
            steps {
                script {
                    docker.build("${JD_IMAGE}")
                }
            }
        }
        stage('Push') {
            steps {
                script {
                    docker.withRegistry("http://${HARBOR_REGISTRY}", 'harbor_credentials') {
                        docker.image("${JD_IMAGE}").push()
                    }
                }
            }
        }
    }
}
