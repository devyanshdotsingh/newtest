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
    }
    
    // post {
    //     always {
    //         // Clean up any resources if needed
    //     }
    // }
}
