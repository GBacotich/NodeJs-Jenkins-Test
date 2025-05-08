pipeline {
  agent any

  environment {
    NODE_ENV = 'test'
  }

  stages {
      stage('Install Dependencies') {
      steps {
        dir('NodeJs-Jenkins-Test') {
          bat 'npm install'
        }
      }
    }

    stage('Run Tests') {
      steps {
        dir('NodeJs-Jenkins-Test') {
          bat 'npm test'  // Optional: prevent full pipeline failure if you want to still collect test reports
          junit 'test-results/*.xml'
        }
      }
    }
  }

  post {
    always {
      dir('NodeJs-Jenkins-Test') {
        archiveArtifacts artifacts: '**/coverage/**', fingerprint: true
      }
    }
  }
}
