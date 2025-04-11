pipeline {
    agent any

    tools {
        nodejs 'node-18'  // 👈 this should match the name you gave in Global Tool Configuration
    }

    environment {
        SONAR_TOKEN = credentials('sonar-token')
    }

    stages {
        stage('Install dependencies') {
            steps {
                sh 'npm install'
            }
        }


        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('My SonarQube Server') {
                    sh "sonar-scanner -Dsonar.login=${SONAR_TOKEN}"
                }
            }
        }
    }
}
