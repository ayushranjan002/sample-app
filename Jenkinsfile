pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Get the latest code from the GitHub repository
                echo 'Checking out code...'
                git 'https://github.com/ayushranjan002/sample-app.git'
            }
        }

        stage('Build Docker Image') {
            steps {
                // Build the Docker image using the Dockerfile in the repo.
                // We will tag it as 'sample-app'
                echo 'Building the Docker image...'
                sh 'docker build -t sample-app:latest .'
            }
        }

        stage('Deploy Locally') {
            steps {
                echo 'Deploying the container locally...'
                
                // Stop and remove any old container with the same name to avoid conflicts
                sh 'docker stop sample-app-container || true'
                sh 'docker rm sample-app-container || true'
                
                // Run the newly built image as a container
                // It will run in the background (-d) and be named 'sample-app-container'
                // We'll map port 3000 on the host to port 3000 in the container (assuming your app.js uses port 3000)
                sh 'docker run -d --name sample-app-container -p 3000:3000 sample-app:latest'
            }
        }
    }
    
    post {
        always {
            echo 'Pipeline finished.'
        }
    }
}