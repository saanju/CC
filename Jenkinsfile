pipeline {
    agent any

    tools {
        dockerTool 'Docker' // Use the Docker tool configured in Jenkins
    }

    environment {
        DOCKER_IMAGE = 'sanj27/user-srv:latest'
    }

    stages {
        stage('Build') {
            steps {
                script {
                     dir('user-service') {
                        docker.build DOCKER_IMAGE
                    }
                }
            }
        }

        // Add other stages as needed
    }
}
