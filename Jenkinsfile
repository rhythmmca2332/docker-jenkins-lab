pipeline {
    agent any

    stages {
        stage('Build Docker Image') {
            steps {
                // Use bat for Windows command to build Docker image
                bat 'docker build -t my-flask-app:latest .'
            }
        }

        stage('Run Docker Container') {
            steps {
                // Use bat command to run Docker container without nohup
                bat 'docker run -d -p 5000:5000 --name my-flask-container my-flask-app:latest'
            }
        }
    }

    post {
        always {
            // Cleanup Docker containers and images
            bat 'docker stop my-flask-container || echo ignored'
            bat 'docker rm my-flask-container || echo ignored'
            bat 'docker rmi my-flask-app:latest || echo ignored'
        }
    }
}
