pipeline {
  agent any

  stages {
    stage('Build') {
      steps {
        echo 'Building...'
      }
    }
    stage('Test') {
      steps {
        echo 'Testing...'
        // 模拟测试失败：你也可以加个 error 'fail' 看失败通知
        // error 'Tests failed'
      }
    }
  }

  post {
    always {
      emailext (
        subject: "Build Status: ${currentBuild.currentResult}",
        body: """<p>Build finished with status: ${currentBuild.currentResult}</p>
                 <p>Check the details at: <a href="${env.BUILD_URL}">${env.BUILD_URL}</a></p>""",
        to: "你的邮箱地址",
        mimeType: 'text/html',
        attachLog: true
      )
    }
  }
}
