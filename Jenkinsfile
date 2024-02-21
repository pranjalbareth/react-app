pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'react-app-image' // Name for your Docker image
        ARTIFACTORY_SERVER_ID = 'artifactory1' // ID of the Artifactory server configured in Jenkins
        DOCKER_REGISTRY = 'docker-trial' // Name of the Docker repository in Artifactory
    }

    stages {
       
        stage('Build Docker Image') {
            steps {
                script {
                    // Build Docker image
                    docker.build(env.DOCKER_IMAGE)
                }
            }
        }

        stage('Push to Artifactory') {
            steps {
                script {
                    // Push Docker image to Artifactory
                    def server = 'https://pranjalbareth.jfrog.io/artifactory/docker-local/'
                    server.publish docker.image("${env.DOCKER_IMAGE}:latest").push(),
                }
            }
        }
    }
}
