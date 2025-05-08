pipeline {
  agent any

  environment {
    NODE_ENV = 'test'
  }

  stages {
    stage('Clone Repo') {
      steps {
        withCredentials([string(credentialsId: 'GITHUB_TOKEN', variable: 'REPO_URL')]) {
          sh 'git clone $REPO_URL'
          // Navigate into the cloned directory if needed
          dir('NodeJs-Jenkins-Test') {
            echo "Repo cloned"
          }
        }
      }
    }

    stage('Install Dependencies') {
      steps {
        dir('NodeJs-Jenkins-Test') {
          sh 'npm install'
        }
      }
    }

    stage('Run Tests') {
      steps {
        dir('NodeJs-Jenkins-Test') {
          sh 'npm test || true'  // Optional: prevent full pipeline failure if you want to still collect test reports
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
