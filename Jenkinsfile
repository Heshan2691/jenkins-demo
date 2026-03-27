pipeline {
    agent any

    tools {
        // This must match the name you gave in Step 2
        maven 'Maven3'
    }

    stages {
        stage('Checkout') {
            steps {
                // Jenkins will automatically pull from the Git repo you define in the UI
                checkout scm
            }
        }

        stage('Build') {
            steps {
                // Compiles code and creates the JAR file
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Test') {
            steps {
                // Runs your unit tests
                sh 'mvn test'
            }
        }

        stage('Deployment Prep') {
            steps {
                echo 'Build and Test complete! The JAR is ready in the target/ folder.'
            }
        }
    }
}