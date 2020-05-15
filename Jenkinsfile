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
        publishHTML([      allowMissing: false,      alwaysLinkToLastBuild: false,      keepAll: true,      reportDir: '',      reportFiles: 'index.html',      reportName: "RCov Report"    ])
      }
    }

    stage('Artifacts Report') {
      steps {
        archiveArtifacts(artifacts: '*/builds/24/htmlreports/*.html', onlyIfSuccessful: true)
      }
    }
  }
}
