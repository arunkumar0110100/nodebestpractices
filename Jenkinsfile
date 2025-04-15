pipeline {
    agent any

    tools {
        nodejs 'node-18' // Make sure this matches the name from Global Tool Configuration
    }

    environment {
        SONAR_TOKEN = credentials('sonar-token') // Optional here, since you're using withCredentials later
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
                    withCredentials([string(credentialsId: 'sonar-token', variable: 'SONAR_TOKEN')]) {
                        sh '''
                          sonar-scanner \
                          -Dsonar.login=$SONAR_TOKEN \
                          -Dsonar.projectKey=test1 \
                          -Dsonar.sources=.
                        '''
                    }
                }
            }
        }
    }
}
