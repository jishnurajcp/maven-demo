pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                echo "Fetching source code..."
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo "Building the application without tests..."
                bat 'mvn clean install -DskipTests'
            }
        }

        stage('Package') {
            steps {
                echo "Packaging application..."
                bat 'mvn package -DskipTests'
            }
            post {
                success {
                    archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
                }
            }
        }
    }

    post {
        success {
            echo "Build completed successfully."
        }
        failure {
            echo "Build failed."
        }
    }
}
