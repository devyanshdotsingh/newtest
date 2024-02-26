pipeline {
    agent {
        node {
            label "linux"
        }
    }
    options{
        buildDiscarder(logRotator(numToKeepStr: '3')) // Retain history on the last 10 builds
        timestamps() // Append timestamps to each line
    }

    stages {
        stage('Checkout') {
            steps {
                // Checkout source code from Git repository
                git branch: 'main', changelog: false, poll: false, url: 'https://github.com/devyanshdotsingh/newtest.git'
            }
        }
        
        stage('Build') {
            agent {
                dockerfile {
                    label 'linux'
                    filename 'Dockerfile'
                    reuseNode true
                }
            }
            steps {
                // Install dependencies and build the Node.js application
                sh 'npm install'
                sh 'npm run build'
            }
        }

        stage('Test') {
            agent {
                dockerfile {
                    label 'linux'
                    filename 'Dockerfile'
                    reuseNode true
                }
            }
            steps {
                // Run tests
                sh 'npm test'
            }
        }
        
        stage('Deploy') {
            environment {
                // Set environment variables for deployment
                //DOCKERHUB_CREDENTIALS = credentials('Jenkins Build')
                DOCKER_IMAGE = 'nodetestimage'
                TAG = 'devyansh'
            }
            steps {

                script{
                //Docker login
                sh 'echo "Puchu@123" | docker login -u devplus2 --password-stdin'
                // Build Docker image
                sh 'docker build -t ${DOCKER_IMAGE}:${TAG} .'
                // Push Docker image to Docker registry
                sh 'docker push artifacts_cicd/${DOCKER_IMAGE}:${TAG}'
                // Deploy Docker image to Kubernetes cluster
                // sh 'kubectl apply -f deployment.yaml'
                }
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
