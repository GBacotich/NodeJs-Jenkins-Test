pipeline {
  agent any

  environment {
    NODE_ENV = 'test'
  }

  stages {
    stage('Install Dependencies') {
      steps {
        sh 'npm install'
      }
    }

    stage('Run Tests') {
      steps {
        sh 'npm test'
        junit 'test-results/*.xml'
      }
    }

    stage('Call GitHub API (Secret Use)') {
      steps {
        withCredentials([string(credentialsId: 'GITHUB_TOKEN', variable: 'TOKEN')]) {
          sh 'curl -H "Authorization: token $TOKEN" https://api.github.com/user'
        }
      }
    }
  }

  post {
    always {
      archiveArtifacts artifacts: '**/coverage/**', fingerprint: true
    }

    failure {
      mail to: 'devops-team@example.com',
           subject: "Build Failed in ${env.JOB_NAME}",
           body: "The build failed. Please check Jenkins."
    }
  }
}
