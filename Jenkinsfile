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

        stage('Run for Verification') {
            steps {
                echo 'Starting app on port 8081 for 10 seconds to verify...'
                // This starts the app, waits 10 seconds, then kills it so the pipeline can finish
                bat "start /B java -jar target/*.jar --server.port=8081"
                bat "timeout /t 10"
                bat "taskkill /F /IM java.exe /T"
            }
        }
    }
}