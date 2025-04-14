pipeline {
    agent any

    tools {
        nodejs 'node-18'            // Matches Global Tool Configuration
    }

    environment {
        SONAR_TOKEN = credentials('sonar-token') // From Jenkins credentials
    }

    stages {
        stage('Install dependencies') {
            steps {
                sh 'npm install'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('My SonarQube Server') { // Installation name from Jenkins config
                    sh "sonar-scanner -Dsonar.login=${SONAR_TOKEN}"
                }
            }
        }
    }
}
