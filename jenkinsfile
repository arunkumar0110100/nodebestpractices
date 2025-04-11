pipeline {
  agent any

  environment {
    SONARQUBE_SERVER = 'SonarQubeCorpServer'
  }

  stages {
    stage('Checkout') {
      steps {
        checkout scm
      }
    }

    stage('Install Dependencies') {
      steps {
        sh 'npm ci'
      }
    }

    stage('Run Tests') {
      steps {
        sh 'npm run test -- --coverage'
      }
    }

    stage('SonarQube Analysis') {
      steps {
        withSonarQubeEnv("${SONARQUBE_SERVER}") {
          sh '''
            sonar-scanner \
              -Dsonar.projectKey=api-testing-tool \
              -Dsonar.sources=src \
              -Dsonar.exclusions=**/node_modules/**,**/__tests__/** \
              -Dsonar.javascript.lcov.reportPaths=coverage/lcov.info
          '''
        }
      }
    }

    stage('Quality Gate') {
      steps {
        timeout(time: 5, unit: 'MINUTES') {
          waitForQualityGate abortPipeline: true
        }
      }
    }
  }
}
