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

        withSonarQubeEnv('My SonarQube Server') {
  withCredentials([string(credentialsId: 'sonar-token', variable: 'SONAR_TOKEN')]) {
    sh """
      sonar-scanner \
      -Dsonar.login=$SONAR_TOKEN \
      -Dsonar.projectKey=test \
      -Dsonar.sources=.
    """
  }
}

    }
}
