pipeline {
    agent any
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Echo') {
            steps {
                echo 'Hello, Jenkins!'
            }
        }
        stage('Docker check') {
            steps {
                sh 'docker --version'
            }
        }
    }
    
    // post {
    //     always {
    //         // Clean up any resources if needed
    //     }
    // }
}
