pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'react-app-image' // Name for your Docker image
        ARTIFACTORY_SERVER_ID = 'artifactory1' // ID of the Artifactory server configured in Jenkins
        DOCKER_REGISTRY = 'docker-local' // Name of the Docker repository in 
        SERVER_URL= 'https://pranjalbareth.jfrog.io/artifactory/docker-local/' //artifactory server url
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
                    def server = Artifactory.server ARTIFACTORY_SERVER_ID
                    def dockerInfo = docker.withRegistry("${env.SERVER_URL}/${env.DOCKER_REGISTRY}", ARTIFACTORY_SERVER_ID) {
                        docker.image("${env.DOCKER_IMAGE}:latest").push()
                    }
                }
            }
        }
    }
}
