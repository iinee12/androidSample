pipeline {
  agent any
  stages {
    stage('Auth') {
      steps {
        sh 'chmod +x gradlew'
      }
    }

    stage('build') {
      steps {
        sh './gradlew --no-daemon assembleDebug --stacktrace'
      }
    }

    stage('Artifacts') {
      steps {
        archiveArtifacts(artifacts: '*/build/**/*.apk', onlyIfSuccessful: true)
      }
    }

    stage('SSH') {
      steps {
        httpRequest 'https://my-json-server.typicode.com/jujumilk3/apitest/posts'
      }
      steps {
          publishHTML (target: [
      allowMissing: false,
      alwaysLinkToLastBuild: false,
      keepAll: true,
      reportDir: 'coverage',
      reportFiles: 'index.html',
      reportName: "RCov Report"
    ])
      }
    }

  }
}
