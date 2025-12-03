pipeline {
    agent any

    environment {
        MAVEN_OPTS = "-Dmaven.test.failure.ignore=false"
    }

    stages {

        stage('Checkout') {
            steps {
                echo "Fetching source code..."
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo "Running Maven build..."
                sh 'mvn clean install'
            }
        }

        stage('Test') {
            steps {
                echo "Executing test cases..."
                sh 'mvn test'
            }
        }

        stage('Package') {
            steps {
                echo "Packaging application..."
                sh 'mvn package'
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
