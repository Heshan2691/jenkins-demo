pipeline {
    agent any

    tools {
        maven 'Maven3'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                // Changed 'sh' to 'bat' for Windows
                bat 'mvn clean package -DskipTests'
            }
        }

        stage('Test') {
            steps {
                // Changed 'sh' to 'bat' for Windows
                bat 'mvn test'
            }
        }

        stage('Deployment Prep') {
            steps {
                echo 'Build and Test complete! The JAR is ready in the target folder.'
            }
        }

        stage('Archive Artifacts') {
             steps {
                 // This tells Jenkins to save the JAR file so you can download it from the UI
                 archiveArtifacts artifacts: 'target/*.jar', fingerprint: true
             }
        }
    }
}