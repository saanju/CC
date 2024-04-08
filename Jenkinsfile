pipeline {
    agent any

    environment {
        DOCKER_IMAGE = 'sanj27/user-srv:latest'
    }

    stages {
         stage('Initialize'){
        def dockerHome = tool 'Docker'
        env.PATH = "${dockerHome}/bin:${env.PATH}"
    }
        stage('Build') {
            steps {
                script {
                    docker.build DOCKER_IMAGE
                }
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                // Add your testing commands here
            }
        }

        stage('Push') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'docker-hub-credentials-id') {
                        docker.image(DOCKER_IMAGE).push('latest')
                    }
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'docker-hub-credentials-id') {
                        docker.image(DOCKER_IMAGE).push('latest')
                        sh 'kubectl apply -f kubernetes-manifests/user-srv/user-srv.yaml'
                    }
                }
            }
        }
    }
}
