pipeline {
  agent any

  stages {
    stage('Build') {
      steps {
        echo 'Building...'
      }
    }
  }

  post {
    success {
      emailext(
        subject: "SUCCESS: Job '${env.JOB_NAME} [#${env.BUILD_NUMBER}]'",
        body: "Good news! Job succeeded.\n\nURL: ${env.BUILD_URL}",
        to: 'xutt9813@gmail.com'
      )
    }
    failure {
      emailext(
        subject: "FAILURE: Job '${env.JOB_NAME} [#${env.BUILD_NUMBER}]'",
        body: "Something went wrong...\n\nCheck here: ${env.BUILD_URL}",
        to: 'xutt9813@gmail.com'
      )
    }
  }
}
