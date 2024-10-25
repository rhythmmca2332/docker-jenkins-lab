pipeline {
    agent any

    stages {
        stage('Build Docker Image') {
            steps {
                script {
                    // Build the Docker image using the Dockerfile
                    def dockerImage = docker.build("my-flask-app:latest")
                }
            }
        }

        stage('Run Docker Container') {
            steps {
                script {
                    // Run a container from the built image in detached (daemon) mode
                    sh 'docker run -d -p 5000:5000 --name my-flask-container my-flask-app:latest'
                }
            }
        }
    }

    post {
        always {
            // Clean up Docker containers and images to save space
            sh 'docker stop my-flask-container || true && docker rm my-flask-container || true'
            sh 'docker rmi my-flask-app:latest || true'
        }
    }
}
