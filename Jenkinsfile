pipeline {
    agent any

    environment {
        HARBOR_REGISTRY = "http://192.168.1.150"
        HARBOR_PROJECT = "view"
        IMAGE_NAME = "view-app"
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/your-repo.git', credentialsId: 'github_token'
            }
        }
        stage('Build') {
            steps {
                script {
                    docker.build("${HARBOR_REGISTRY}/${HARBOR_PROJECT}/${IMAGE_NAME}:latest")
                }
            }
        }
        stage('Push') {
            steps {
                script {
                    docker.withRegistry("${HARBOR_REGISTRY}", 'harbor_credentials') {
                        docker.image("${HARBOR_REGISTRY}/${HARBOR_PROJECT}/${IMAGE_NAME}:latest").push()
                    }
                }
            }
        }
    }
}
