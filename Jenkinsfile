pipeline {
    agent {
        docker {
            image 'ubuntu:20.04' // Specify the Docker image to use
            args '-u root' // Optional: Specify additional arguments for the Docker container
        }
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout source code from Git repository
                git branch: 'main', url: 'https://github.com/devyanshdotsingh/newtest.git'
            }
        }
        
        stage('Build') {
            steps {
                // Install dependencies and build the Node.js application
                sh 'npm install'
                sh 'npm run build'
            }
        }

        stage('Test') {
            steps {
                // Run tests
                sh 'npm test'
            }
        }
        
        stage('Deploy') {
            environment {
                // Set environment variables for deployment
                DOCKER_IMAGE = 'nodeimagetest'
            }
            steps {
                // Build Docker image
                sh 'docker build -t $DOCKER_IMAGE .'
                
                // Push Docker image to Docker registry
                sh 'docker push $DOCKER_IMAGE'
                
                // Deploy Docker image to Kubernetes cluster
                sh 'kubectl apply -f deployment.yaml'
            }
        }
    }
    
    post {
        success {
            // Notification for successful build and deployment
            echo 'Build and deployment successful!'
        }
        failure {
            // Notification for failed build or deployment
            echo 'Build or deployment failed!'
        }
    }
}
