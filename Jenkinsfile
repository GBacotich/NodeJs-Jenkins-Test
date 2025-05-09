pipeline {
  agent any

  environment {
    NODE_ENV = 'test'
    JEST_JUNIT_OUTPUT_DIR = 'test-results'
    JEST_JUNIT_OUTPUT_NAME = 'results.xml'
    JEST_JUNIT_OUTPUT = 'test-results/results.xml'
  }

  stages {
    stage('Install Dependencies') {
      steps {
        dir('NodeJs-Jenkins-Test') {
          bat 'npm ci'
        }
      }
    }

    stage('Run Tests') {
      steps {
        dir('NodeJs-Jenkins-Test') {
          bat 'npm test'
        }
      }
    }

    stage('Publish Test Results') {
      steps {
        dir('NodeJs-Jenkins-Test') {
          junit 'test-results/results.xml'
        }
      }
    }
  }

  post {
    always {
      dir('NodeJs-Jenkins-Test') {
        archiveArtifacts artifacts: 'coverage/**', fingerprint: true
      }
    }
  }
}
